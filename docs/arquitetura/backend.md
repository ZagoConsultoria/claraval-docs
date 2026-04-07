# Arquitetura Backend

**Repositório:** [ZagoConsultoria/claraval-back](https://github.com/ZagoConsultoria/claraval-back)

## Stack

| Componente | Versão/Detalhe |
|------------|----------------|
| Java | 17 (compilação), JDK 21 (deploy) |
| Spring Boot | 3.5.6 |
| Build | Maven (mvnw) |
| Banco de Dados | PostgreSQL (produção), H2 (testes) |
| ORM | Spring Data JPA + Hibernate 6.6 |
| Migrações | Flyway (SQL em `db/migration/`) |
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
│   ├── controller/               # Auth, Admin, Arquivo, Status, Usuário
│   ├── dto/                      # arquivo/, auth/, usuario/
│   ├── exception/                # GlobalExceptionHandler, ApiError
│   ├── model/                    # Arquivo, Usuário, Categoria, Token*, Role
│   ├── repository/               # 6 repositories
│   ├── security/                 # SecurityConfig, JwtService, JwtFilter
│   ├── service/                  # Auth, Email, Storage, Password, Usuário
│   └── util/                     # EntityHelper, ChecksumUtil
│
└── newversion/                   # Pacote atual — toda lógica de domínio
    ├── controller/               # 23 controllers REST
    ├── dto/                      # 17 DTOs (Java records)
    ├── model/                    # 25+ entidades + enums/ + pk/
    ├── repository/               # 24 repositories
    └── service/                  # 18 services
```

## Segurança

### Endpoints Públicos (sem auth)

| Método | Path | Descrição |
|--------|------|-----------|
| POST | `/auth/**` | Login, registro, refresh, reset senha |
| GET | `/status` | Health check |
| GET | `/videos/stream/**` | Streaming de vídeo |
| GET | `/live/hls/**` | Proxy HLS da live |
| POST | `/leads` | Captação de leads (landing page) |

### Endpoints Admin Only (`ROLE_ADMIN`)

| Path | Descrição |
|------|-----------|
| `/admin/**` | Gestão de usuários |
| `GET /documents/alldocs` | Listar todos documentos |
| `POST /documents/download-batch` | Download em lote |

### Demais endpoints

Requerem autenticação (`Bearer token` no header).

### CORS

Origins permitidas:

- `http://localhost:3000`
- `https://app.academiaclaraval.com.br`

## Controllers

### Pacote Legado (`app/controller/`)

| Controller | Responsabilidade |
|------------|-----------------|
| `AuthController` | Login, registro, OAuth, refresh, reset senha |
| `AdminController` | CRUD de usuários (admin) |
| `ArquivoController` | Upload/download de arquivos |
| `UsuarioController` | Perfil do usuário logado |
| `StatusController` | Health check |

### Pacote Atual (`newversion/controller/`)

| Controller | Responsabilidade |
|------------|-----------------|
| `SchoolController` | CRUD de escolas |
| `DiagnosticConfigController` | Configuração do diagnóstico (pilares, eixos, perguntas) |
| `DiagnosticExecutionController` | Preenchimento e finalização do diagnóstico |
| `MethodologyController` | Leitura da metodologia (pilares, eixos) |
| `ActionPlanController` | Plano de ação (itens, status, ferramentas vinculadas) |
| `ActionPlanTemplateController` | Templates de plano de ação |
| `ToolController` | Ferramentas de gestão (template, score, checklist) |
| `VideoController` | Vídeos (CRUD, progresso) |
| `VideoStreamController` | Streaming de vídeo (HTTP Range) |
| `AdminVideoController` | Gestão admin de vídeos |
| `TrailController` | Trilhas de e-learning (usuário) |
| `AdminTrailController` | CRUD de trilhas (admin) |
| `LiveController` | Status da live |
| `LiveHlsProxyController` | Proxy HLS para MediaMTX |
| `SharedDocumentController` | Upload/download de documentos |
| `DocumentCategoryController` | Categorias de documentos |
| `SprintController` | CRUD de sprints |
| `TarefaController` | CRUD de tarefas |
| `BannerController` | CRUD de banners |
| `EventController` | CRUD de eventos |
| `LeadController` | Captação de leads |
| `ReportsController` | Relatórios e métricas admin |
| `AppConfigController` | Configurações do app |

## DTOs

Java records com validação Jakarta. Padrão de mapeamento:

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
| `Cluster` | ATE_300, DE_300_A_500, DE_500_A_1000, ACIMA_DE_1000 |
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
| `FeedbackType` | BUG, SUGESTAO |

<!-- TODO: Screenshot do Swagger UI (/swagger-ui.html) — referência visual da API interativa -->
