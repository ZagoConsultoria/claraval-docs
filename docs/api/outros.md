# API - Outros Endpoints

## Banners

**Prefixo:** `/banners`
**Autenticacao:** Requerida

### GET /banners

Lista banners ativos (filtrados por periodo de exibicao).

### POST /banners

Cria banner. **Admin only.**

**Request:** `multipart/form-data`

| Campo | Tipo | Descricao |
|-------|------|-----------|
| `image` | File | Imagem do banner |
| `title` | string | Titulo |
| `linkUrl` | string | URL de destino (opcional) |
| `startDate` | date | Data inicio exibicao |
| `endDate` | date | Data fim exibicao |
| `sortOrder` | number | Ordem no carrossel |

### PUT /banners/{id}

Atualiza banner. **Admin only.**

### DELETE /banners/{id}

Remove banner. **Admin only.**

### PATCH /banners/{id}/toggle

Ativa/desativa banner. **Admin only.**

## Eventos

**Prefixo:** `/events`
**Autenticacao:** Requerida

### GET /events

Lista eventos.

### POST /events

Cria evento. **Admin only.**

**Request:**

```json
{
  "title": "Mentoria Semanal",
  "description": "Sessao de mentoria sobre estrategia",
  "startDate": "2026-04-10T14:00:00",
  "endDate": "2026-04-10T15:00:00",
  "meetingLink": "https://teams.microsoft.com/...",
  "targetSchools": ["uuid-1", "uuid-2"]
}
```

### PUT /events/{id}

Atualiza evento. **Admin only.**

### DELETE /events/{id}

Remove evento. **Admin only.**

## Leads

**Prefixo:** `/leads`

### POST /leads

Captura lead da landing page. **Publico.**

**Request:**

```json
{
  "nome": "Joao Silva",
  "email": "joao@escola.com",
  "whatsapp": "61999999999",
  "escola": "Colegio Exemplo",
  "cargo": "Diretor",
  "numAlunos": "300-500",
  "produtoInteresse": "Club",
  "mensagem": "Gostaria de saber mais",
  "utmSource": "google",
  "utmMedium": "cpc",
  "utmCampaign": "gestao-escolar"
}
```

### GET /leads

Lista leads capturados. **Admin only.**

## Reports

**Prefixo:** `/reports`
**Autenticacao:** `ROLE_ADMIN`

### GET /reports/dashboard

Retorna metricas do painel admin:

- Total de diagnosticos (com media de score)
- Ferramentas utilizadas
- Aulas assistidas
- Escolas ativas
- Usuarios ativos

### GET /reports/escola/{escolaId}

Retorna metricas especificas de uma escola.

## App Config

**Prefixo:** `/app-config`
**Autenticacao:** `ROLE_ADMIN`

### GET /app-config

Retorna configuracoes gerais do app.

### PUT /app-config

Atualiza configuracoes.

## Health Check

### GET /status

Retorna status do servidor. **Publico.**

**Response (200):**

```json
{
  "status": "UP"
}
```
