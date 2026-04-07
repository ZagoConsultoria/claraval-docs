# Arquitetura Backend

**Repositorio:** [ZagoConsultoria/claraval-back](https://github.com/ZagoConsultoria/claraval-back)

## Stack

| Componente | Versao/Detalhe |
|------------|----------------|
| Java | 17 (compilacao), JDK 21 (deploy) |
| Spring Boot | 3.5.6 |
| Build | Maven (mvnw) |
| Banco de Dados | PostgreSQL (producao), H2 (testes) |
| ORM | Spring Data JPA + Hibernate 6.6 |
| Migracoes | Flyway (SQL em `db/migration/`) |
| Auth | Spring Security 6 + JWT (jjwt 0.11.5) + Google OAuth |
| API Docs | SpringDoc OpenAPI 2.6.0 (Swagger UI) |
| Email | Spring Boot Mail (Gmail SMTP) |
| PDF | iText 2.1.7 |
| Excel | Apache POI 5.2.3 |
| Mapeamento | ModelMapper 3.2.0 + MapStruct 1.5.5 |
| WebSocket | spring-boot-starter-websocket |
| Templates | Thymeleaf (email) |
| Monitoramento | Spring Boot Actuator |

## Estrutura de Pacotes

```
com.example.claravalback/
├── ClaravalBackApplication.java
├── app/                          # Pacote legado
│   ├── config/                   # CorsConfig
│   ├── controller/               # Auth, Admin, Arquivo, Status, Usuario
│   ├── dto/                      # arquivo/, auth/, usuario/
│   ├── exception/                # GlobalExceptionHandler, ApiError
│   ├── model/                    # Arquivo, Usuario, Categoria, Token*, Role
│   ├── repository/               # 6 repositories
│   ├── security/                 # SecurityConfig, JwtService, JwtFilter
│   ├── service/                  # Auth, Email, Storage, Password, Usuario
│   └── util/                     # EntityHelper, ChecksumUtil
│
└── newversion/                   # Pacote atual — toda logica de dominio
    ├── controller/               # 23 controllers REST
    ├── dto/                      # 17 DTOs (Java records)
    ├── model/                    # 25+ entidades + enums/ + pk/
    ├── repository/               # 24 repositories
    └── service/                  # 18 services
```

## Seguranca

### Endpoints Publicos (sem auth)

| Metodo | Path | Descricao |
|--------|------|-----------|
| POST | `/auth/**` | Login, registro, refresh, reset senha |
| GET | `/status` | Health check |
| GET | `/videos/stream/**` | Streaming de video |
| GET | `/live/hls/**` | Proxy HLS da live |
| POST | `/leads` | Captacao de leads (landing page) |

### Endpoints Admin Only (`ROLE_ADMIN`)

| Path | Descricao |
|------|-----------|
| `/admin/**` | Gestao de usuarios |
| `GET /documents/alldocs` | Listar todos documentos |
| `POST /documents/download-batch` | Download em lote |

### Demais endpoints

Requerem autenticacao (`Bearer token` no header).

### CORS

Origins permitidas:

- `http://localhost:3000`
- `https://app.academiaclaraval.com.br`

## Controllers

### Pacote Legado (`app/controller/`)

| Controller | Responsabilidade |
|------------|-----------------|
| `AuthController` | Login, registro, OAuth, refresh, reset senha |
| `AdminController` | CRUD de usuarios (admin) |
| `ArquivoController` | Upload/download de arquivos |
| `UsuarioController` | Perfil do usuario logado |
| `StatusController` | Health check |

### Pacote Atual (`newversion/controller/`)

| Controller | Responsabilidade |
|------------|-----------------|
| `SchoolController` | CRUD de escolas |
| `DiagnosticConfigController` | Configuracao do diagnostico (pilares, eixos, perguntas) |
| `DiagnosticExecutionController` | Preenchimento e finalizacao do diagnostico |
| `MethodologyController` | Leitura da metodologia (pilares, eixos) |
| `ActionPlanController` | Plano de acao (itens, status, ferramentas vinculadas) |
| `ActionPlanTemplateController` | Templates de plano de acao |
| `ToolController` | Ferramentas de gestao (template, score, checklist) |
| `VideoController` | Videos (CRUD, progresso) |
| `VideoStreamController` | Streaming de video (HTTP Range) |
| `AdminVideoController` | Gestao admin de videos |
| `TrailController` | Trilhas de e-learning (usuario) |
| `AdminTrailController` | CRUD de trilhas (admin) |
| `LiveController` | Status da live |
| `LiveHlsProxyController` | Proxy HLS para MediaMTX |
| `SharedDocumentController` | Upload/download de documentos |
| `DocumentCategoryController` | Categorias de documentos |
| `SprintController` | CRUD de sprints |
| `TarefaController` | CRUD de tarefas |
| `BannerController` | CRUD de banners |
| `EventController` | CRUD de eventos |
| `LeadController` | Captacao de leads |
| `ReportsController` | Relatorios e metricas admin |
| `AppConfigController` | Configuracoes do app |

## DTOs

Java records com validacao Jakarta. Padrao de mapeamento:

```java
public record SchoolResponse(UUID id, String name, ...) {
    public static SchoolResponse toResponse(School school) {
        return new SchoolResponse(school.getId(), school.getName(), ...);
    }
}
```

## Enums

| Enum | Valores |
|------|---------|
| `ContractType` | CLUBE, CORP, START |
| `DiagnosticStatus` | EM_ANDAMENTO, FINALIZADO |
| `ActionPlanStatus` | PENDENTE, EM_ANDAMENTO, CONCLUIDO |
| `ToolType` | TEMPLATE, SCORE, CHECKLIST |
| `VideoProgressStatus` | NAO_INICIADO, EM_ANDAMENTO, ASSISTIDO |
| `VideoProvider` | UPLOAD, YOUTUBE, VIMEO, LIVE_RECORDING |
| `TargetAudience` | CLUBE, CORP, START, AMBOS |
| `SprintStatus` | ABERTA, FECHADA |
| `SprintTamanho` | SEMANAL, QUINZENAL |
| `TarefaStatus` | A_FAZER, FAZENDO, CONCLUIDO |
| `TarefaOrigem` | SPRINT, PLANO_CLA |
| `Priority` | ALTA, MEDIA, BAIXA |
| `DocumentDirection` | UPLOAD, DOWNLOAD |

<!-- TODO: Screenshot do Swagger UI (/swagger-ui.html) — referencia visual da API interativa -->
