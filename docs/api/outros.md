# API - Outros Endpoints

## Banners

**Prefixo:** `/banners`
**Autenticação:** Requerida

### GET /banners

Lista banners ativos (filtrados por período de exibição).

### POST /banners

Cria banner. **Admin only.**

**Request:** `multipart/form-data`

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `image` | File | Imagem do banner |
| `title` | string | Título |
| `linkUrl` | string | URL de destino (opcional) |
| `startDate` | date | Data início exibição |
| `endDate` | date | Data fim exibição |
| `sortOrder` | number | Ordem no carrossel |

### PUT /banners/{id}

Atualiza banner. **Admin only.**

### DELETE /banners/{id}

Remove banner. **Admin only.**

### PATCH /banners/{id}/toggle

Ativa/desativa banner. **Admin only.**

## Eventos

**Prefixo:** `/events`
**Autenticação:** Requerida

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

Captura lead da landing page. **Público.**

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
**Autenticação:** `ROLE_ADMIN`

### GET /reports/dashboard

Retorna métricas do painel admin:

- Total de diagnósticos (com média de score)
- Ferramentas utilizadas
- Aulas assistidas
- Escolas ativas
- Usuários ativos

### GET /reports/escola/{escolaId}

Retorna métricas específicas de uma escola.

## App Config

**Prefixo:** `/app-config`
**Autenticação:** `ROLE_ADMIN`

### GET /app-config

Retorna configurações gerais do app.

### PUT /app-config

Atualiza configurações.

## Health Check

### GET /status

Retorna status do servidor. **Público.**

**Response (200):**

```json
{
  "status": "UP"
}
```
