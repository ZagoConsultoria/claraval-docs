# Banco de Dados

**SGBD:** PostgreSQL
**Schema:** `claraval`
**Migracoes:** Flyway (`src/main/resources/db/migration/`)
**ORM:** Spring Data JPA + Hibernate 6.6

## Entidades Principais

### Autenticacao e Usuarios

| Entidade | Descricao |
|----------|-----------|
| `Usuario` | Usuarios do sistema (admin ou cliente). Campos: nome, email, role, escola vinculada |
| `Role` | Papeis: ROLE_ADMIN, ROLE_USER |
| `TokenSessao` | Refresh tokens para manter sessao |
| `TokenResetSenha` | Tokens de reset de senha com expiracao |
| `AuditoriaLogin` | Log de tentativas de login |

### Escolas e Contratos

| Entidade | Descricao |
|----------|-----------|
| `School` | Escola cliente. Campos: nome, endereco, logo, contractType (CLUBE/CORP/START), cluster, selectedPillarId (START) |

### Diagnostico e Metodologia

| Entidade | Descricao |
|----------|-----------|
| `Pillar` | Os 5 pilares da metodologia |
| `Axis` | Eixos dentro de cada pilar |
| `Question` | Perguntas do diagnostico, vinculadas a um eixo |
| `QuestionLevel` | Descricao de cada nivel (1-5) de cada pergunta |
| `Diagnostic` | Diagnostico de uma escola (status, notas, data) |
| `DiagnosticAnswer` | Resposta a uma pergunta (nivel selecionado, observacoes) |

### Plano de Acao

| Entidade | Descricao |
|----------|-----------|
| `ActionPlanItem` | Item do plano de acao (descricao, prioridade, status, pilar, eixo) |
| `ActionPlanTemplate` | Template para geracao automatica de itens |

### Ferramentas

| Entidade | Descricao |
|----------|-----------|
| `Tool` | Ferramenta de gestao (tipo: TEMPLATE, SCORE, CHECKLIST) |
| `ToolSubmission` | Preenchimento de uma ferramenta por escola (versionado, JSON) |

### E-Learning

| Entidade | Descricao |
|----------|-----------|
| `Video` | Video com titulo, descricao, pilar, cluster, provider |
| `VideoProgress` | Progresso de visualizacao por usuario (PK composta: VideoProgressPK) |
| `Trail` | Trilha de aprendizado |
| `TrailVideo` | Relacao N:N entre Trail e Video (com ordem) |

### Tarefas e Sprints

| Entidade | Descricao |
|----------|-----------|
| `Sprint` | Sprint da escola (nome, datas, tamanho, status) |
| `Tarefa` | Tarefa vinculada a sprint ou plano CLA |
| `Subtarefa` | Subtarefas dentro de uma tarefa |
| `TarefaHistorico` | Historico de alteracoes de status |

### Documentos

| Entidade | Descricao |
|----------|-----------|
| `Categoria` | Categoria de documento vinculada a um pilar |
| `Arquivo` | Documento enviado pela escola |
| `SharedDocument` | Documentos compartilhados (com folders) |
| `DocumentFolder` | Pastas para organizacao de documentos |

### Outros

| Entidade | Descricao |
|----------|-----------|
| `Banner` | Banners do carrossel do dashboard |
| `Event` | Eventos/encontros agendados |
| `Lead` | Leads capturados pela landing page |
| `AppConfig` | Configuracoes gerais do app |
| `DiagnosticPriority` | Prioridades customizadas por tipo de contrato |
| `DiagnosticSession` | Sessoes de preenchimento compartilhado |

## Diagrama ER Simplificado

```mermaid
erDiagram
    School ||--o{ Usuario : "tem"
    School ||--o{ Diagnostic : "realiza"
    School ||--o{ Sprint : "tem"
    School ||--o{ ToolSubmission : "preenche"

    Diagnostic ||--o{ DiagnosticAnswer : "contem"
    Diagnostic ||--o{ ActionPlanItem : "gera"

    Pillar ||--o{ Axis : "contem"
    Axis ||--o{ Question : "contem"
    Question ||--o{ QuestionLevel : "tem niveis"
    Question ||--o{ DiagnosticAnswer : "respondida em"

    Trail ||--o{ TrailVideo : "agrupa"
    Video ||--o{ TrailVideo : "pertence a"
    Video ||--o{ VideoProgress : "progresso"

    Sprint ||--o{ Tarefa : "contem"
    Tarefa ||--o{ Subtarefa : "tem"

    Categoria ||--o{ Arquivo : "organiza"
```

## Convencoes

- **IDs**: UUID em todas as entidades
- **BaseEntity**: Classe base no pacote `newversion/model/` com campos comuns
- **Toggleable**: Interface para entidades com campo `active` (uso com `EntityHelper.toggleActive()`)
- **Schema**: Todas as tabelas no schema `claraval`
- **Nomenclatura DB**: Colunas em portugues (legado), migrando para ingles no pacote `newversion`
