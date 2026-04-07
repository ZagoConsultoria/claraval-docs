# API - E-Learning

## Vídeos

**Prefixo:** `/videos`
**Autenticação:** Requerida (exceto streaming)

### GET /videos

Lista vídeos disponíveis para o usuário.

**Query params:**

| Param | Tipo | Descrição |
|-------|------|-----------|
| `pillar` | string | Filtro por pilar |
| `cluster` | string | Filtro por cluster (tamanho da escola) |

### GET /videos/{id}

Retorna detalhes do vídeo.

### GET /videos/stream/{filename}

Stream de vídeo com suporte a HTTP Range (seeking). **Público.**

### POST /videos/{id}/progresso

Salva progresso de visualização.

**Request:**

```json
{
  "currentTime": 125.5,
  "duration": 600.0,
  "status": "EM_ANDAMENTO"
}
```

Status muda para `ASSISTIDO` automaticamente quando progresso >= 90%.

### GET /videos/continue-watching

Retorna vídeos com progresso parcial (seção "Continue Assistindo" do dashboard).

## Gestão de Vídeos (Admin)

**Prefixo:** `/admin/videos` ou `/videos` (dependendo do endpoint)
**Autenticação:** `ROLE_ADMIN`

### POST /videos

Cria vídeo com upload de arquivo.

**Request:** `multipart/form-data`

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `file` | File | Arquivo de vídeo (MP4, MOV, WebM, AVI) |
| `title` | string | Título do vídeo |
| `description` | string | Descrição |
| `pillarIds` | string[] | IDs dos pilares |
| `clusters` | string[] | Clusters (tamanhos de escola) |
| `duration` | number | Duração em segundos |

### PUT /videos/{id}

Atualiza metadados do vídeo.

### DELETE /videos/{id}

Remove vídeo. **Admin only.**

### PATCH /videos/{id}/toggle

Ativa/desativa vídeo.

## Trilhas

**Prefixo:** `/trails`
**Autenticação:** Requerida

### GET /trails

Lista trilhas disponíveis para o usuário com progresso.

**Response (200):**

```json
[
  {
    "id": "uuid",
    "title": "Fundamentos de Estrategia",
    "description": "Aprenda os fundamentos...",
    "icon": "target",
    "order": 1,
    "videos": [...],
    "progress": 45.5,
    "active": true
  }
]
```

### GET /trails/{id}

Retorna trilha com lista completa de vídeos e progresso individual.

## Gestão de Trilhas (Admin)

**Prefixo:** `/admin/trails`
**Autenticação:** `ROLE_ADMIN`

### POST /admin/trails

Cria trilha.

### PUT /admin/trails/{id}

Atualiza trilha (título, descrição, ordem).

### DELETE /admin/trails/{id}

Remove trilha.

### PUT /admin/trails/{id}/videos

Define os vídeos da trilha com ordenação.

**Request:**

```json
{
  "videoIds": ["uuid-1", "uuid-2", "uuid-3"]
}
```

A ordem dos IDs define a ordem de exibição.

## Regras para Contratos Start

- No dashboard e "Continue Assistindo", só aparecem vídeos do pilar permitido
- Na página de e-learning, trilhas bloqueadas aparecem com ícone de cadeado
- Na tela de detalhe da trilha bloqueada, exibe tela de "Acesso Restrito"
