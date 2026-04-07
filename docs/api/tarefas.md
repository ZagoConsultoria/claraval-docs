# API - Tarefas e Sprints

## Sprints

**Prefixo:** `/sprints`
**Autenticação:** Requerida

### GET /sprints/escola/{escolaId}

Lista sprints da escola.

**Response (200):**

```json
[
  {
    "id": "uuid",
    "name": "Sprint 1 - Marco",
    "startDate": "2026-03-01",
    "endDate": "2026-03-14",
    "tamanho": "QUINZENAL",
    "status": "ABERTA",
    "escolaId": "uuid"
  }
]
```

### POST /sprints

Cria nova sprint. **Admin only.**

**Request:**

```json
{
  "name": "Sprint 2 - Marco",
  "startDate": "2026-03-15",
  "endDate": "2026-03-28",
  "tamanho": "QUINZENAL",
  "escolaId": "uuid"
}
```

### PUT /sprints/{id}

Atualiza sprint.

### PATCH /sprints/{id}/fechar

Fecha sprint (ABERTA → FECHADA). Tarefas ficam read-only.

### DELETE /sprints/{id}

Remove sprint. **Admin only.**

## Tarefas

**Prefixo:** `/tarefas`
**Autenticação:** Requerida

### GET /tarefas/escola/{escolaId}

Lista tarefas da escola.

**Query params:**

| Param | Tipo | Descrição |
|-------|------|-----------|
| `sprintId` | UUID | Filtro por sprint |
| `status` | string | A_FAZER, FAZENDO, CONCLUIDO |
| `origem` | string | SPRINT, PLANO_CLA |
| `responsavelId` | UUID | Filtro por responsável |

**Response (200):**

```json
[
  {
    "id": "uuid",
    "titulo": "Implementar funil de matriculas",
    "descricao": "...",
    "origem": "SPRINT",
    "sprintId": "uuid",
    "responsavel": { "id": "uuid", "nome": "Maria" },
    "status": "A_FAZER",
    "pokerPoints": 5,
    "prazo": "2026-03-10",
    "pirata": false,
    "krReference": "Aumentar conversao em 20%",
    "subtarefas": [
      { "id": "uuid", "titulo": "Mapear etapas", "concluida": false }
    ]
  }
]
```

### POST /tarefas

Cria nova tarefa.

**Request:**

```json
{
  "titulo": "Implementar funil de matriculas",
  "descricao": "Mapear todas as etapas do funil",
  "origem": "SPRINT",
  "sprintId": "uuid",
  "responsavelId": "uuid",
  "pokerPoints": 5,
  "prazo": "2026-03-10",
  "pirata": false,
  "krReference": "Aumentar conversao em 20%",
  "escolaId": "uuid"
}
```

### PUT /tarefas/{id}

Atualiza tarefa. Todos os campos editáveis por qualquer usuário autenticado (admin ou cliente).

### DELETE /tarefas/{id}

Remove tarefa. **Admin only.**

### PATCH /tarefas/{id}/status

Altera status da tarefa (também pode ser feito via drag-and-drop no kanban).

**Request:**

```json
{
  "status": "FAZENDO"
}
```

### POST /tarefas/{id}/subtarefas

Cria subtarefa.

### PATCH /tarefas/{tarefaId}/subtarefas/{subtarefaId}/toggle

Marca/desmarca subtarefa como concluída.

### DELETE /tarefas/{tarefaId}/subtarefas/{subtarefaId}

Remove subtarefa.

## Regras de Negócio

- Sprint fechada: tarefas ficam read-only
- Dropdown de responsáveis inclui usuários da escola + todos os admins
- Tarefas de origem `PLANO_CLA` são itens do plano de ação exibidos como read-only
- Analytics calculam: pontos planejados vs concluídos, velocidade por sprint, taxa de conclusão
