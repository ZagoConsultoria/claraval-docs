# API - Escolas

**Prefixo:** `/escolas`
**Autenticacao:** Requerida (Admin para CRUD, Usuario para leitura da propria escola)

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
    "cluster": "300-500",
    "contractStartDate": "2026-01-15",
    "selectedPillarId": null,
    "overallScore": 3.8,
    "active": true
  }
]
```

### GET /escolas/{id}

Retorna detalhes de uma escola especifica.

### POST /escolas

Cria nova escola. **Admin only.**

**Request:**

```json
{
  "name": "Nova Escola",
  "address": "Rua B, 456",
  "contractType": "CORP",
  "focusSector": "Comercial",
  "cluster": "500-1000",
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

## Campos Especificos por Contrato

| Campo | Start | Club | Corp |
|-------|-------|------|------|
| `selectedPillarId` | Obrigatorio | null | null |
| `focusSector` | null | null | Opcional |
| Duracao | 3 meses | 12 meses | 12 meses |
