# API - E-Learning

## Videos

**Prefixo:** `/videos`
**Autenticacao:** Requerida (exceto streaming)

### GET /videos

Lista videos disponiveis para o usuario.

**Query params:**

| Param | Tipo | Descricao |
|-------|------|-----------|
| `pillar` | string | Filtro por pilar |
| `cluster` | string | Filtro por cluster (tamanho da escola) |

### GET /videos/{id}

Retorna detalhes do video.

### GET /videos/stream/{filename}

Stream de video com suporte a HTTP Range (seeking). **Publico.**

### POST /videos/{id}/progresso

Salva progresso de visualizacao.

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

Retorna videos com progresso parcial (secao "Continue Assistindo" do dashboard).

## Gestao de Videos (Admin)

**Prefixo:** `/admin/videos` ou `/videos` (dependendo do endpoint)
**Autenticacao:** `ROLE_ADMIN`

### POST /videos

Cria video com upload de arquivo.

**Request:** `multipart/form-data`

| Campo | Tipo | Descricao |
|-------|------|-----------|
| `file` | File | Arquivo de video (MP4, MOV, WebM, AVI) |
| `title` | string | Titulo do video |
| `description` | string | Descricao |
| `pillarIds` | string[] | IDs dos pilares |
| `clusters` | string[] | Clusters (tamanhos de escola) |
| `duration` | number | Duracao em segundos |

### PUT /videos/{id}

Atualiza metadados do video.

### DELETE /videos/{id}

Remove video. **Admin only.**

### PATCH /videos/{id}/toggle

Ativa/desativa video.

## Trilhas

**Prefixo:** `/trails`
**Autenticacao:** Requerida

### GET /trails

Lista trilhas disponiveis para o usuario com progresso.

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

Retorna trilha com lista completa de videos e progresso individual.

## Gestao de Trilhas (Admin)

**Prefixo:** `/admin/trails`
**Autenticacao:** `ROLE_ADMIN`

### POST /admin/trails

Cria trilha.

### PUT /admin/trails/{id}

Atualiza trilha (titulo, descricao, ordem).

### DELETE /admin/trails/{id}

Remove trilha.

### PUT /admin/trails/{id}/videos

Define os videos da trilha com ordenacao.

**Request:**

```json
{
  "videoIds": ["uuid-1", "uuid-2", "uuid-3"]
}
```

A ordem dos IDs define a ordem de exibicao.

## Regras para Contratos Start

- No dashboard e "Continue Assistindo", so aparecem videos do pilar permitido
- Na pagina de e-learning, trilhas bloqueadas aparecem com icone de cadeado
- Na tela de detalhe da trilha bloqueada, exibe tela de "Acesso Restrito"
