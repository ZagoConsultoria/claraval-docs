# Git e CI/CD

## Branches

| Branch | Propósito |
|--------|-----------|
| `main` | Produção — deploy automático via GitHub Actions |

!!! warning "Atenção"
    Push para `main` dispara deploy automático em produção. Não há branch de staging.

## CI/CD

Ambos os repositórios usam GitHub Actions com runner **self-hosted** (`[self-hosted, claraval]`) em servidor Windows.

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

**Otimização**: `npm install` só executa se `package.json` ou `package-lock.json` mudaram no último commit.

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

**Nota**: Testes são pulados no deploy (`-DskipTests`) para reduzir tempo de downtime.

## Serviços Windows (NSSM)

| Serviço | Porta | Diretório |
|---------|-------|-----------|
| `claraval-front` | 3000 | `C:\apps\app1-frontend\claraval-front` |
| `claraval-back` | 3001 | `C:\apps\app1-backend\claraval-back` |

Comandos úteis (no servidor):

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
- Tamanho máximo: 10MB
- Histórico: 5 arquivos
- Nível root: INFO
- Nível aplicação: DEBUG

### Frontend

- Logs do Next.js no stdout do serviço NSSM
- Acessíveis via Event Viewer do Windows ou output do NSSM
