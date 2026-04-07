# API - Escolas

**Prefixo:** `/escolas`
**Autenticação:** Requerida (Admin para CRUD, Usuário para leitura da própria escola)

## Endpoints

### GET /escolas

Lista todas as escolas. **Admin only.**

**Response (200):**

```json
[
  {
    "id": "uuid",
    "name": "Colegio Exemplo",
    "address": "Rua A, 123",
    "logoUrl": "/uploads/logos/escola.png",
    "contractType": "CLUBE",
    "cluster": "DE_300_A_500",
    "contractStartDate": "2026-01-15",
    "selectedPillarId": null,
    "overallScore": 3.8,
    "active": true
  }
]
```

### GET /escolas/{id}

Retorna detalhes de uma escola específica.

### POST /escolas

Cria nova escola. **Admin only.**

**Request:**

```json
{
  "name": "Nova Escola",
  "address": "Rua B, 456",
  "contractType": "CORP",
  "focusSector": "Comercial",
  "cluster": "DE_500_A_1000",
  "contractStartDate": "2026-03-01"
}
```

Para contratos **Start**, incluir:

```json
{
  "contractType": "START",
  "selectedPillarId": "uuid-do-pilar"
}
```

### PUT /escolas/{id}

Atualiza dados da escola. **Admin only.**

### DELETE /escolas/{id}

Remove escola. **Admin only.**

### PATCH /escolas/{id}/toggle

Ativa/desativa escola. **Admin only.**

## Campos Específicos por Contrato

| Campo | Start | Club | Corp |
|-------|-------|------|------|
| `cluster` | Obrigatório (enum) | Obrigatório (enum) | Obrigatório (enum) |
| `selectedPillarId` | Obrigatório | null | null |
| `focusSector` | null | null | Opcional |
| Duração | 3 meses | 12 meses | 12 meses |

## Enum Cluster

| Valor | Descrição |
|-------|-----------|
| `ATE_300` | Até 300 alunos |
| `DE_300_A_500` | De 300 a 500 alunos |
| `DE_500_A_1000` | De 500 a 1000 alunos |
| `ACIMA_DE_1000` | Acima de 1000 alunos |
