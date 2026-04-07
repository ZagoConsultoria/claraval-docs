# Setup Backend

## Pre-requisitos

- **JDK 17+** (recomendado JDK 21)
- **Maven 3.9+** (ou usar o wrapper `./mvnw`)
- **PostgreSQL** rodando e acessivel

## Instalacao

```bash
git clone https://github.com/ZagoConsultoria/claraval-back.git
cd claraval-back
./mvnw clean package -DskipTests
java -jar target/claraval-back-*.jar
# → http://localhost:3001
```

## Configuracao

O arquivo `src/main/resources/application.properties` contem as configuracoes do banco, JWT, email, etc.

Propriedades principais:

| Propriedade | Descricao |
|-------------|-----------|
| `spring.datasource.url` | URL do PostgreSQL |
| `spring.datasource.username` | Usuario do banco |
| `spring.datasource.password` | Senha do banco |
| `app.jwt.secret` | Chave secreta JWT |
| `app.jwt.access-minutes` | Duracao do access token (default: 1440 = 24h) |
| `app.jwt.refresh-days` | Duracao do refresh token (default: 90 dias) |
| `google.client-id` | Client ID do Google OAuth |
| `spring.mail.username` | Email SMTP |
| `spring.mail.password` | Senha do app SMTP |
| `storage.local.path` | Diretorio de uploads (default: `./uploads`) |
| `app.frontend-url` | URL do frontend para links em emails |

!!! danger "Seguranca"
    O arquivo `application.properties` contem credenciais em texto plano no repositorio. Para desenvolvimento local, crie um `application-local.properties` com suas credenciais e rode com `--spring.profiles.active=local`.

## Banco de Dados

As migracoes Flyway sao executadas automaticamente ao iniciar a aplicacao.

Arquivos de migracao em: `src/main/resources/db/migration/`

O schema JPA esta configurado como `validate` — a estrutura do banco deve ser gerenciada pelas migracoes, nao pelo Hibernate.

## API Docs (Swagger)

Com o backend rodando, acesse:

**[http://localhost:3001/swagger-ui.html](http://localhost:3001/swagger-ui.html)**

Documentacao interativa de todos os endpoints com schemas de request/response.

<!-- TODO: Screenshot do Swagger UI — ajuda devs frontend a entender os endpoints disponiveis -->

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
├── app/                   # Pacote legado (auth, usuarios, arquivos)
│   ├── security/          # SecurityConfig, JWT, filtros
│   ├── service/           # AuthService, EmailService, etc.
│   └── util/              # EntityHelper (OBRIGATORIO usar)
│
└── newversion/            # Pacote atual (toda logica de dominio)
    ├── controller/        # 23 endpoints REST
    ├── service/           # 18 services
    ├── model/             # 25+ entidades JPA
    ├── model/enums/       # Enums de status/tipo
    ├── repository/        # 24 repositories
    └── dto/               # Java records com validacao
```

## MediaMTX (Live Streaming)

Se precisar testar live streaming:

1. Baixe o [MediaMTX](https://github.com/bluenviron/mediamtx)
2. Use o `mediamtx.yml` da raiz do repositorio
3. Inicie: `./mediamtx`
4. Configure OBS para enviar RTMP para `rtmp://localhost:1935/live`
