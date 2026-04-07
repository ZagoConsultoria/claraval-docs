# API - Usuários

## Gestão de Usuários (Admin)

**Prefixo:** `/admin`
**Autenticação:** Requerida (`ROLE_ADMIN`)

### GET /admin/usuarios

Lista todos os usuários com filtros opcionais.

**Query params:**

| Param | Tipo | Descrição |
|-------|------|-----------|
| `search` | string | Busca por nome ou email |
| `role` | string | Filtro por role (ROLE_ADMIN, ROLE_USER) |
| `escolaId` | UUID | Filtro por escola |

### POST /admin/usuarios

Cria novo usuário. Envia email de boas-vindas automaticamente.

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

Atualiza dados do usuário.

### DELETE /admin/usuarios/{id}

Remove usuário.

### PATCH /admin/usuarios/{id}/toggle

Ativa/desativa usuário.

### GET /admin/users/{id}/categorias

Retorna categorias de documentos configuradas para o usuário.

### PUT /admin/users/{id}/categorias

Atualiza permissões de categorias de documentos do usuário.

**Request:**

```json
{
  "categoriaIds": ["uuid-1", "uuid-2"]
}
```

Lista vazia = acesso irrestrito (backward-compatible).

## Perfil do Usuário

**Prefixo:** `/usuarios`
**Autenticação:** Requerida (qualquer role)

### GET /usuarios/perfil

Retorna dados do usuário logado.

### PUT /usuarios/perfil

Atualiza perfil do usuário logado (nome, senha).

### PUT /usuarios/completar-perfil

Completa perfil após primeiro login (define senha para usuários criados pelo admin).
