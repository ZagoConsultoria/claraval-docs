# API - Visão Geral

**Base URL:** `http://localhost:3001` (dev) | `https://app.academiaclaraval.com.br` (prod)

**Swagger UI:** [http://localhost:3001/swagger-ui.html](http://localhost:3001/swagger-ui.html) (com backend rodando)

## Autenticação

Todas as requisições autenticadas devem incluir o header:

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

## Códigos de Status

| Código | Significado |
|--------|-------------|
| 200 | Sucesso |
| 201 | Criado com sucesso |
| 400 | Requisição inválida (validação) |
| 401 | Não autenticado |
| 403 | Sem permissão |
| 404 | Recurso não encontrado |
| 500 | Erro interno |

## Permissões

| Role | Acesso |
|------|--------|
| `ROLE_ADMIN` | Todas as rotas, todas as escolas |
| `ROLE_USER` | Apenas dados da própria escola |

## Endpoints por Domínio

| Domínio | Prefixo | Documentação |
|---------|---------|--------------|
| Autenticação | `/auth` | [Ver detalhes](autenticacao.md) |
| Escolas | `/escolas` | [Ver detalhes](escolas.md) |
| Usuários | `/admin`, `/usuarios` | [Ver detalhes](usuarios.md) |
| Diagnóstico | `/diagnostics`, `/methodology` | [Ver detalhes](diagnostico.md) |
| Plano de Ação | `/action-plans`, `/action-plan-templates` | [Ver detalhes](plano-de-acao.md) |
| Ferramentas | `/tools` | [Ver detalhes](ferramentas.md) |
| E-Learning | `/videos`, `/trails` | [Ver detalhes](elearning.md) |
| Documentos | `/documents`, `/arquivos` | [Ver detalhes](documentos.md) |
| Tarefas | `/sprints`, `/tarefas` | [Ver detalhes](tarefas.md) |
| Live | `/live` | [Ver detalhes](live.md) |
| Outros | `/banners`, `/events`, `/leads`, `/reports` | [Ver detalhes](outros.md) |

## Upload de Arquivos

Uploads usam `multipart/form-data`. Limite configurado: **3GB** por arquivo.

Formatos aceitos para vídeo: MP4, MOV, WebM, AVI.
Formatos aceitos para documentos: PDF, XLSX, DOCX, PNG, JPG.
