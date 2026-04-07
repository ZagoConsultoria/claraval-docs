# Git e CI/CD

## Branches

| Branch | Proposito |
|--------|-----------|
| `main` | Producao — deploy automatico via GitHub Actions |

!!! warning "Atencao"
    Push para `main` dispara deploy automatico em producao. Nao ha branch de staging.

## CI/CD

Ambos os repositorios usam GitHub Actions com runner **self-hosted** (`[self-hosted, claraval]`) em servidor Windows.

### Frontend — Deploy Flow

```yaml
on:
  push:
    branches: [main]

steps:
  1. git pull origin main
  2. npm install (se package.json mudou)
  3. npm run build
  4. nssm restart claraval-front
  5. Health check em http://localhost:3000
```

**Otimizacao**: `npm install` so executa se `package.json` ou `package-lock.json` mudaram no ultimo commit.

### Backend — Deploy Flow

```yaml
on:
  push:
    branches: [main]

steps:
  1. git pull origin main
  2. nssm stop claraval-back
  3. mvn clean package -DskipTests
  4. nssm start claraval-back
  5. Health check em http://localhost:3001/status (10 tentativas, 3s entre cada)
```

**Nota**: Testes sao pulados no deploy (`-DskipTests`) para reduzir tempo de downtime.

## Servicos Windows (NSSM)

| Servico | Porta | Diretorio |
|---------|-------|-----------|
| `claraval-front` | 3000 | `C:\apps\app1-frontend\claraval-front` |
| `claraval-back` | 3001 | `C:\apps\app1-backend\claraval-back` |

Comandos uteis (no servidor):

```powershell
# Status
C:\nssm\nssm.exe status claraval-front
C:\nssm\nssm.exe status claraval-back

# Restart
C:\nssm\nssm.exe restart claraval-front
C:\nssm\nssm.exe restart claraval-back

# Logs do backend
Get-Content -Tail 50 C:\apps\app1-backend\claraval-back\logs\claraval-back.log
```

## Logs

### Backend

- Arquivo: `logs/claraval-back.log`
- Tamanho maximo: 10MB
- Historico: 5 arquivos
- Nivel root: INFO
- Nivel aplicacao: DEBUG

### Frontend

- Logs do Next.js no stdout do servico NSSM
- Acessiveis via Event Viewer do Windows ou output do NSSM
