# API - Plano de Acao

## Itens do Plano

**Prefixo:** `/action-plans`
**Autenticacao:** Requerida

### GET /action-plans/escola/{escolaId}

Lista itens do plano de acao da escola.

**Query params:**

| Param | Tipo | Descricao |
|-------|------|-----------|
| `pillar` | string | Filtro por pilar |
| `status` | string | PENDENTE, EM_ANDAMENTO, CONCLUIDO |

**Response (200):**

```json
[
  {
    "id": "uuid",
    "description": "Formalizar planejamento estrategico",
    "pillar": "Estrategia",
    "axis": "Planejamento",
    "priority": "ALTA",
    "status": "PENDENTE",
    "dueDate": "2026-06-30",
    "completedAt": null,
    "suggestedTools": [...],
    "suggestedVideos": [...],
    "diagnosticId": "uuid"
  }
]
```

### PUT /action-plans/{id}

Atualiza item do plano. **Admin only** para edicao completa; Cliente pode alterar apenas `status`.

### PATCH /action-plans/{id}/status

Altera status do item (Cliente pode usar).

**Request:**

```json
{
  "status": "CONCLUIDO"
}
```

### POST /action-plans

Cria novo item manualmente. **Admin only.**

### DELETE /action-plans/{id}

Remove item. **Admin only.**

## Templates

**Prefixo:** `/action-plan-templates`
**Autenticacao:** `ROLE_ADMIN`

Templates definem quais itens sao gerados automaticamente apos um diagnostico.

### GET /action-plan-templates

Lista todos os templates.

### POST /action-plan-templates

Cria template.

**Request:**

```json
{
  "description": "Implementar BSC",
  "pillarId": "uuid",
  "axisId": "uuid",
  "questionId": "uuid",
  "minLevel": 1,
  "maxLevel": 3,
  "priority": "ALTA",
  "contractType": "CLUBE",
  "suggestedToolIds": ["uuid"],
  "suggestedVideoIds": ["uuid"]
}
```

**Logica:** Quando a escola responde entre `minLevel` e `maxLevel` na pergunta vinculada, o item e gerado no plano.

**`contractType`:** Quando preenchido, template so gera para escolas com aquele contrato. Quando null, gera para todos.

### PUT /action-plan-templates/{id}

Atualiza template.

### DELETE /action-plan-templates/{id}

Remove template.

## Regras de Negocio

- Itens gerados automaticamente apos `PATCH /diagnostics/{id}/finalizar`
- Prioridade baseada na nota: menores notas = maior prioridade
- Para contratos Start: ferramentas e aulas de pilares fora do selecionado aparecem bloqueadas no frontend (visíveis mas nao acessiveis)
- Admin pode vincular ferramentas e aulas sugeridas a cada item
