# API - Ferramentas

**Prefixo:** `/tools`
**Autenticacao:** Requerida

## Tipos de Ferramentas

| Tipo | Descricao |
|------|-----------|
| `TEMPLATE` | Formulario estruturado para documentar informacoes (ex: Mapa Estrategico BSC) |
| `SCORE` | Auto-avaliacao com calculo de nota/score (ex: Check de Posicionamento Competitivo) |
| `CHECKLIST` | Lista de itens com checkbox e progresso (ex: Jornada do Aluno) |

## Endpoints

### GET /tools

Lista ferramentas disponiveis para a escola do usuario.

**Query params:**

| Param | Tipo | Descricao |
|-------|------|-----------|
| `pillar` | string | Filtro por pilar |
| `type` | string | TEMPLATE, SCORE, CHECKLIST |

**Response (200):**

```json
[
  {
    "id": "uuid",
    "name": "Mapa Estrategico (BSC)",
    "description": "Construa o mapa estrategico da escola...",
    "type": "TEMPLATE",
    "pillar": "Estrategia",
    "contractType": "CLUBE",
    "config": { ... },
    "active": true
  }
]
```

### GET /tools/{id}

Retorna detalhes da ferramenta com configuracao completa.

### POST /tools

Cria nova ferramenta. **Admin only.**

### PUT /tools/{id}

Atualiza ferramenta. **Admin only.**

### PATCH /tools/{id}/toggle

Ativa/desativa ferramenta. **Admin only.**

## Submissions (Preenchimentos)

### GET /tools/{id}/submissions?escolaId={escolaId}

Lista preenchimentos da escola para uma ferramenta (historico de versoes).

### POST /tools/{id}/submissions

Salva preenchimento (cria nova versao).

**Request:**

```json
{
  "escolaId": "uuid",
  "data": {
    "campo1": "valor1",
    "campo2": "valor2",
    "tabela": [
      { "col1": "a", "col2": "b" }
    ]
  }
}
```

### GET /tools/submissions/{submissionId}/pdf

Exporta preenchimento em PDF.

## Regras de Negocio

- Liberacao hibrida: tipo de contrato define set base + admin pode liberar/bloquear por escola
- Preenchimentos sao versionados (novo submit cria nova versao, nao sobrescreve)
- Auto-save no frontend via debounce de 2 segundos
- Campo `config` contem a estrutura do formulario (JSON schema)
