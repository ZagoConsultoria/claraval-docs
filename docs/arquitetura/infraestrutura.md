# Infraestrutura

## Ambiente de Produção

| Componente | Detalhe |
|------------|---------|
| **Servidor** | Windows (self-hosted) |
| **Gerenciador de serviços** | NSSM (Non-Sucking Service Manager) |
| **Frontend** | Serviço `claraval-front` em `C:\apps\app1-frontend\claraval-front` (porta 3000) |
| **Backend** | Serviço `claraval-back` em `C:\apps\app1-backend\claraval-back` (porta 3001) |
| **Banco de Dados** | PostgreSQL na porta 5433 |
| **Live Streaming** | MediaMTX (RTMP porta 1935 → HLS) |
| **CI/CD** | GitHub Actions com self-hosted runner |
| **Domínio** | `app.academiaclaraval.com.br` |

## CI/CD

Ambos os repositórios usam GitHub Actions com runner self-hosted (`[self-hosted, claraval]`) que executa no servidor Windows de produção.

### Deploy Frontend

```
Push para main
  → Pull do código
    → npm install (apenas se package.json mudou)
      → npm run build
        → NSSM restart claraval-front
          → Health check em http://localhost:3000
```

### Deploy Backend

```
Push para main
  → Pull do código
    → NSSM stop claraval-back
      → mvn clean package -DskipTests
        → NSSM start claraval-back
          → Health check em http://localhost:3001/status
```

!!! warning "Atenção"
    O deploy é automático no push para `main`. Não há ambiente de staging. Qualquer merge em main vai direto para produção.

## MediaMTX (Live Streaming)

Servidor de streaming open-source que converte RTMP para HLS.

**Fluxo:**

```
OBS Studio (Professor)
  → RTMP (porta 1935) → MediaMTX
    → HLS → Backend (proxy) → Frontend (hls.js)
```

- Capacidade: ~30 alunos simultâneos
- Configuração: `mediamtx.yml` na raiz do backend
- Gerenciado via NSSM como serviço Windows

## Variáveis de Ambiente

### Frontend

| Variável | Descrição | Default |
|----------|-----------|---------|
| `NEXT_PUBLIC_API_URL` | URL do backend | `http://localhost:3001` |
| `NEXT_PUBLIC_GOOGLE_CLIENT_ID` | Client ID do Google OAuth | — |
| `NEXT_PUBLIC_APP_NAME` | Nome exibido no app | `Claraval Academy` |

### Backend

Configurado via `application.properties`:

| Propriedade | Descrição |
|-------------|-----------|
| `spring.datasource.url` | URL do PostgreSQL |
| `spring.datasource.username/password` | Credenciais do banco |
| `app.jwt.secret` | Chave secreta para assinar tokens JWT |
| `app.jwt.access-minutes` | Duração do access token (1440 min = 24h) |
| `app.jwt.refresh-days` | Duração do refresh token (90 dias) |
| `google.client-id` | Client ID do Google OAuth |
| `spring.mail.username/password` | Credenciais SMTP (Gmail) |
| `storage.local.path` | Diretório de uploads |
| `app.frontend-url` | URL do frontend (para links em emails) |

!!! danger "Segurança"
    Atualmente `application.properties` contém credenciais em texto plano. Recomendação: migrar para variáveis de ambiente ou Spring Cloud Config/Vault.

## Monitoramento

- **Actuator**: Spring Boot Actuator habilitado
- **Logs**: Arquivo em `logs/claraval-back.log` (max 10MB, 5 arquivos históricos)
- **Health check**: `GET /status` retorna 200 quando o backend está saudável
