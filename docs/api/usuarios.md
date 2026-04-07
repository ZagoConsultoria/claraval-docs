# API - Usuarios

## Gestao de Usuarios (Admin)

**Prefixo:** `/admin`
**Autenticacao:** Requerida (`ROLE_ADMIN`)

### GET /admin/usuarios

Lista todos os usuarios com filtros opcionais.

**Query params:**

| Param | Tipo | Descricao |
|-------|------|-----------|
| `search` | string | Busca por nome ou email |
| `role` | string | Filtro por role (ROLE_ADMIN, ROLE_USER) |
| `escolaId` | UUID | Filtro por escola |

### POST /admin/usuarios

Cria novo usuario. Envia email de boas-vindas automaticamente.

**Request:**

```json
{
  "nome": "Maria Silva",
  "email": "maria@escola.com",
  "cargo": "Diretora",
  "escolaId": "uuid",
  "role": "ROLE_USER"
}
```

### PUT /admin/usuarios/{id}

Atualiza dados do usuario.

### DELETE /admin/usuarios/{id}

Remove usuario.

### PATCH /admin/usuarios/{id}/toggle

Ativa/desativa usuario.

### GET /admin/users/{id}/categorias

Retorna categorias de documentos configuradas para o usuario.

### PUT /admin/users/{id}/categorias

Atualiza permissoes de categorias de documentos do usuario.

**Request:**

```json
{
  "categoriaIds": ["uuid-1", "uuid-2"]
}
```

Lista vazia = acesso irrestrito (backward-compatible).

## Perfil do Usuario

**Prefixo:** `/usuarios`
**Autenticacao:** Requerida (qualquer role)

### GET /usuarios/perfil

Retorna dados do usuario logado.

### PUT /usuarios/perfil

Atualiza perfil do usuario logado (nome, senha).

### PUT /usuarios/completar-perfil

Completa perfil apos primeiro login (define senha para usuarios criados pelo admin).
