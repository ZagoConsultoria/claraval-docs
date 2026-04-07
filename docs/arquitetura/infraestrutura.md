# Infraestrutura

## Ambiente de Producao

| Componente | Detalhe |
|------------|---------|
| **Servidor** | Windows (self-hosted) |
| **Gerenciador de servicos** | NSSM (Non-Sucking Service Manager) |
| **Frontend** | Servico `claraval-front` em `C:\apps\app1-frontend\claraval-front` (porta 3000) |
| **Backend** | Servico `claraval-back` em `C:\apps\app1-backend\claraval-back` (porta 3001) |
| **Banco de Dados** | PostgreSQL na porta 5433 |
| **Live Streaming** | MediaMTX (RTMP porta 1935 → HLS) |
| **CI/CD** | GitHub Actions com self-hosted runner |
| **Dominio** | `app.academiaclaraval.com.br` |

## CI/CD

Ambos os repositorios usam GitHub Actions com runner self-hosted (`[self-hosted, claraval]`) que executa no servidor Windows de producao.

### Deploy Frontend

```
Push para main
  → Pull do codigo
    → npm install (apenas se package.json mudou)
      → npm run build
        → NSSM restart claraval-front
          → Health check em http://localhost:3000
```

### Deploy Backend

```
Push para main
  → Pull do codigo
    → NSSM stop claraval-back
      → mvn clean package -DskipTests
        → NSSM start claraval-back
          → Health check em http://localhost:3001/status
```

!!! warning "Atencao"
    O deploy e automatico no push para `main`. Nao ha ambiente de staging. Qualquer merge em main vai direto para producao.

## MediaMTX (Live Streaming)

Servidor de streaming open-source que converte RTMP para HLS.

**Fluxo:**

```
OBS Studio (Professor)
  → RTMP (porta 1935) → MediaMTX
    → HLS → Backend (proxy) → Frontend (hls.js)
```

- Capacidade: ~30 alunos simultaneos
- Configuracao: `mediamtx.yml` na raiz do backend
- Gerenciado via NSSM como servico Windows

## Variaveis de Ambiente

### Frontend

| Variavel | Descricao | Default |
|----------|-----------|---------|
| `NEXT_PUBLIC_API_URL` | URL do backend | `http://localhost:3001` |
| `NEXT_PUBLIC_GOOGLE_CLIENT_ID` | Client ID do Google OAuth | — |
| `NEXT_PUBLIC_APP_NAME` | Nome exibido no app | `Claraval Academy` |

### Backend

Configurado via `application.properties`:

| Propriedade | Descricao |
|-------------|-----------|
| `spring.datasource.url` | URL do PostgreSQL |
| `spring.datasource.username/password` | Credenciais do banco |
| `app.jwt.secret` | Chave secreta para assinar tokens JWT |
| `app.jwt.access-minutes` | Duracao do access token (1440 min = 24h) |
| `app.jwt.refresh-days` | Duracao do refresh token (90 dias) |
| `google.client-id` | Client ID do Google OAuth |
| `spring.mail.username/password` | Credenciais SMTP (Gmail) |
| `storage.local.path` | Diretorio de uploads |
| `app.frontend-url` | URL do frontend (para links em emails) |

!!! danger "Seguranca"
    Atualmente `application.properties` contem credenciais em texto plano. Recomendacao: migrar para variaveis de ambiente ou Spring Cloud Config/Vault.

## Monitoramento

- **Actuator**: Spring Boot Actuator habilitado
- **Logs**: Arquivo em `logs/claraval-back.log` (max 10MB, 5 arquivos historicos)
- **Health check**: `GET /status` retorna 200 quando o backend esta saudavel
