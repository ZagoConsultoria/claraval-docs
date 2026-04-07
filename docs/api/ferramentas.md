# API - Ferramentas

**Prefixo:** `/tools`
**Autenticação:** Requerida

## Tipos de Ferramentas

| Tipo | Descrição |
|------|-----------|
| `TEMPLATE` | Formulário estruturado para documentar informações (ex: Mapa Estratégico BSC) |
| `SCORE` | Auto-avaliação com cálculo de nota/score (ex: Check de Posicionamento Competitivo) |
| `CHECKLIST` | Lista de itens com checkbox e progresso (ex: Jornada do Aluno) |

## Endpoints

### GET /tools

Lista ferramentas disponíveis para a escola do usuário.

**Query params:**

| Param | Tipo | Descrição |
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

Retorna detalhes da ferramenta com configuração completa.

### POST /tools

Cria nova ferramenta. **Admin only.**

### PUT /tools/{id}

Atualiza ferramenta. **Admin only.**

### PATCH /tools/{id}/toggle

Ativa/desativa ferramenta. **Admin only.**

## Submissions (Preenchimentos)

### GET /tools/{id}/submissions?escolaId={escolaId}

Lista preenchimentos da escola para uma ferramenta (histórico de versões).

### POST /tools/{id}/submissions

Salva preenchimento (cria nova versão).

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

## Regras de Negócio

- Liberação híbrida: tipo de contrato define set base + admin pode liberar/bloquear por escola
- Preenchimentos são versionados (novo submit cria nova versão, não sobrescreve)
- Auto-save no frontend via debounce de 2 segundos
- Campo `config` contém a estrutura do formulário (JSON schema)
