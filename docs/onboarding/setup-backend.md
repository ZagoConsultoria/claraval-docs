# Setup Backend

## Pré-requisitos

- **JDK 17+** (recomendado JDK 21)
- **Maven 3.9+** (ou usar o wrapper `./mvnw`)
- **PostgreSQL** rodando e acessível

## Instalação

```bash
git clone https://github.com/ZagoConsultoria/claraval-back.git
cd claraval-back
./mvnw clean package -DskipTests
java -jar target/claraval-back-*.jar
# → http://localhost:3001
```

## Configuração

O arquivo `src/main/resources/application.properties` contém as configurações do banco, JWT, email, etc.

Propriedades principais:

| Propriedade | Descrição |
|-------------|-----------|
| `spring.datasource.url` | URL do PostgreSQL |
| `spring.datasource.username` | Usuário do banco |
| `spring.datasource.password` | Senha do banco |
| `app.jwt.secret` | Chave secreta JWT |
| `app.jwt.access-minutes` | Duração do access token (default: 1440 = 24h) |
| `app.jwt.refresh-days` | Duração do refresh token (default: 90 dias) |
| `google.client-id` | Client ID do Google OAuth |
| `spring.mail.username` | Email SMTP |
| `spring.mail.password` | Senha do app SMTP |
| `storage.local.path` | Diretório de uploads (default: `./uploads`) |
| `app.frontend-url` | URL do frontend para links em emails |

!!! danger "Segurança"
    O arquivo `application.properties` contém credenciais em texto plano no repositório. Para desenvolvimento local, crie um `application-local.properties` com suas credenciais e rode com `--spring.profiles.active=local`.

## Banco de Dados

As migrações Flyway são executadas automaticamente ao iniciar a aplicação.

Arquivos de migração em: `src/main/resources/db/migration/`

O schema JPA está configurado como `validate` — a estrutura do banco deve ser gerenciada pelas migrações, não pelo Hibernate.

## API Docs (Swagger)

Com o backend rodando, acesse:

**[http://localhost:3001/swagger-ui.html](http://localhost:3001/swagger-ui.html)**

Documentação interativa de todos os endpoints com schemas de request/response.

<!-- TODO: Screenshot do Swagger UI — ajuda devs frontend a entender os endpoints disponíveis -->

## Scripts

```bash
./mvnw clean package                  # Build completo
./mvnw clean package -DskipTests      # Build sem testes
./mvnw test                           # Rodar testes
./mvnw spring-boot:run                # Rodar em dev
```

## Estrutura de Pastas Relevantes

```
src/main/java/com/example/claravalback/
├── app/                   # Pacote legado (auth, usuários, arquivos)
│   ├── security/          # SecurityConfig, JWT, filtros
│   ├── service/           # AuthService, EmailService, etc.
│   └── util/              # EntityHelper (OBRIGATÓRIO usar)
│
└── newversion/            # Pacote atual (toda lógica de domínio)
    ├── controller/        # 23 endpoints REST
    ├── service/           # 18 services
    ├── model/             # 25+ entidades JPA
    ├── model/enums/       # Enums de status/tipo
    ├── repository/        # 24 repositories
    └── dto/               # Java records com validação
```

## MediaMTX (Live Streaming)

Se precisar testar live streaming:

1. Baixe o [MediaMTX](https://github.com/bluenviron/mediamtx)
2. Use o `mediamtx.yml` da raiz do repositório
3. Inicie: `./mediamtx`
4. Configure OBS para enviar RTMP para `rtmp://localhost:1935/live`
