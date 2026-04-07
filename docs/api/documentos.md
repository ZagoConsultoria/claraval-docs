# API - Documentos

## Categorias

**Prefixo:** `/documents/categories` ou `/categorias`
**Autenticacao:** Requerida

### GET /categorias/minhas

Retorna categorias que o usuario tem permissao de acessar.

Quando o usuario nao tem restricoes configuradas (tabela vazia), retorna todas as categorias.

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
**Autenticacao:** Requerida

### GET /documents/escola

Lista documentos da escola do usuario, filtrados pelas categorias permitidas (server-side).

### POST /arquivos/upload

Upload de documento.

**Request:** `multipart/form-data`

| Campo | Tipo | Descricao |
|-------|------|-----------|
| `file` | File | Arquivo (PDF, XLSX, DOCX, PNG, JPG) |
| `categoriaId` | UUID | Categoria do documento |

!!! note "Validacao de acesso"
    O upload valida se o usuario tem acesso a categoria antes de salvar. Retorna 403 se nao permitido.

### GET /documents/download/{id}

Download de documento. Valida acesso por categoria — retorna 403 se nao permitido.

### GET /documents/alldocs

Lista todos os documentos de todas as escolas. **Admin only.**

### POST /documents/download-batch

Download em lote (ZIP). **Admin only.**

## Controle de Acesso por Categoria

O acesso a categorias de documentos e configurado por usuario:

- Tabela `usuario_categorias` (many-to-many)
- Tabela vazia = acesso irrestrito (backward-compatible)
- Admin sempre ve todos os documentos
- Toda filtragem e **server-side** — frontend apenas renderiza o que recebe

Configuracao via endpoints admin:

- `GET /admin/users/{id}/categorias` — consulta permissoes
- `PUT /admin/users/{id}/categorias` — atualiza permissoes (lista vazia = irrestrito)
