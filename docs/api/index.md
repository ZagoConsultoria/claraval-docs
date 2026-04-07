# API - Visao Geral

**Base URL:** `http://localhost:3001` (dev) | `https://app.academiaclaraval.com.br` (prod)

**Swagger UI:** [http://localhost:3001/swagger-ui.html](http://localhost:3001/swagger-ui.html) (com backend rodando)

## Autenticacao

Todas as requisicoes autenticadas devem incluir o header:

```
Authorization: Bearer <accessToken>
```

O `accessToken` expira em 24 horas. Use o endpoint de refresh para obter um novo.

## Formato de Resposta

**Sucesso:** Retorna o objeto ou lista diretamente (sem wrapper).

**Erro:**

```json
{
  "mensagem": "Descricao do erro",
  "status": 400
}
```

## Codigos de Status

| Codigo | Significado |
|--------|-------------|
| 200 | Sucesso |
| 201 | Criado com sucesso |
| 400 | Requisicao invalida (validacao) |
| 401 | Nao autenticado |
| 403 | Sem permissao |
| 404 | Recurso nao encontrado |
| 500 | Erro interno |

## Permissoes

| Role | Acesso |
|------|--------|
| `ROLE_ADMIN` | Todas as rotas, todas as escolas |
| `ROLE_USER` | Apenas dados da propria escola |

## Endpoints por Dominio

| Dominio | Prefixo | Documentacao |
|---------|---------|--------------|
| Autenticacao | `/auth` | [Ver detalhes](autenticacao.md) |
| Escolas | `/escolas` | [Ver detalhes](escolas.md) |
| Usuarios | `/admin`, `/usuarios` | [Ver detalhes](usuarios.md) |
| Diagnostico | `/diagnostics`, `/methodology` | [Ver detalhes](diagnostico.md) |
| Plano de Acao | `/action-plans`, `/action-plan-templates` | [Ver detalhes](plano-de-acao.md) |
| Ferramentas | `/tools` | [Ver detalhes](ferramentas.md) |
| E-Learning | `/videos`, `/trails` | [Ver detalhes](elearning.md) |
| Documentos | `/documents`, `/arquivos` | [Ver detalhes](documentos.md) |
| Tarefas | `/sprints`, `/tarefas` | [Ver detalhes](tarefas.md) |
| Live | `/live` | [Ver detalhes](live.md) |
| Outros | `/banners`, `/events`, `/leads`, `/reports` | [Ver detalhes](outros.md) |

## Upload de Arquivos

Uploads usam `multipart/form-data`. Limite configurado: **3GB** por arquivo.

Formatos aceitos para video: MP4, MOV, WebM, AVI.
Formatos aceitos para documentos: PDF, XLSX, DOCX, PNG, JPG.
