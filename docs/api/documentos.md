# API - Documentos

## Categorias

**Prefixo:** `/documents/categories` ou `/categorias`
**Autenticação:** Requerida

### GET /categorias/minhas

Retorna categorias que o usuário tem permissão de acessar.

Quando o usuário não tem restrições configuradas (tabela vazia), retorna todas as categorias.

### GET /categorias

Lista todas as categorias. **Admin only.**

### POST /categorias

Cria nova categoria. **Admin only.**

**Request:**

```json
{
  "nome": "NPS Trimestral",
  "pillar": "Resultados",
  "descricao": "Envie o relatorio de NPS do trimestre",
  "obrigatorio": true,
  "active": true
}
```

### PUT /categorias/{id}

Atualiza categoria. **Admin only.**

### PATCH /categorias/{id}/toggle

Ativa/desativa categoria. **Admin only.**

## Upload e Download

**Prefixo:** `/documents` ou `/arquivos`
**Autenticação:** Requerida

### GET /documents/escola

Lista documentos da escola do usuário, filtrados pelas categorias permitidas (server-side).

### POST /arquivos/upload

Upload de documento.

**Request:** `multipart/form-data`

| Campo | Tipo | Descrição |
|-------|------|-----------|
| `file` | File | Arquivo (PDF, XLSX, DOCX, PNG, JPG) |
| `categoriaId` | UUID | Categoria do documento |

!!! note "Validação de acesso"
    O upload valida se o usuário tem acesso a categoria antes de salvar. Retorna 403 se não permitido.

### GET /documents/download/{id}

Download de documento. Valida acesso por categoria — retorna 403 se não permitido.

### GET /documents/alldocs

Lista todos os documentos de todas as escolas. **Admin only.**

### POST /documents/download-batch

Download em lote (ZIP). **Admin only.**

## Controle de Acesso por Categoria

O acesso a categorias de documentos é configurado por usuário:

- Tabela `usuario_categorias` (many-to-many)
- Tabela vazia = acesso irrestrito (backward-compatible)
- Admin sempre vê todos os documentos
- Toda filtragem é **server-side** — frontend apenas renderiza o que recebe

Configuração via endpoints admin:

- `GET /admin/users/{id}/categorias` — consulta permissões
- `PUT /admin/users/{id}/categorias` — atualiza permissões (lista vazia = irrestrito)
