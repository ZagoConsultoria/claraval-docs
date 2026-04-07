# Padroes Obrigatorios — Backend

Regras extraidas do `CLAUDE.md` do repositorio [claraval-back](https://github.com/ZagoConsultoria/claraval-back).

## Limites de Tamanho

| Elemento | Limite |
|----------|--------|
| Dependencias injetadas por service | Max 5 |
| Linhas por metodo | Max 40 |
| Linhas por arquivo de service | Max ~250 |

Se exceder dependencias, decompor em services menores.

## Entity Lookup

- **Proibido**: `new EntityNotFoundException("string literal")`
- **Obrigatorio**: `EntityHelper.findOrThrow(repo, id, "NomeEntidade")`

```java
// ERRADO
School school = schoolRepository.findById(id)
    .orElseThrow(() -> new EntityNotFoundException("Escola nao encontrada"));

// CORRETO
School school = EntityHelper.findOrThrow(schoolRepository, id, "School");
```

O `EntityHelper` esta em `app/util/EntityHelper.java`.

## Toggle de Ativo

Entidades com campo `active` devem:

1. Implementar interface `Toggleable`
2. Usar `EntityHelper.toggleActive(repo, id, "NomeEntidade")`

Nao reimplementar logica de toggle manualmente.

## Exception Handling

- **Proibido**: `catch (Exception e)` generico (exceto infraestrutura I/O justificada)
- **Obrigatorio**: catch de excecoes especificas

```java
// ERRADO
try { ... } catch (Exception e) { ... }

// CORRETO
try { ... } catch (EntityNotFoundException e) { ... }
try { ... } catch (IOException e) { ... }
```

## Strings e Enums

- **Proibido**: strings hardcoded para status (`"ASSISTIDO"`, `"EM_ANDAMENTO"`)
- **Obrigatorio**: usar enums correspondentes

```java
// ERRADO
video.setStatus("ASSISTIDO");

// CORRETO
video.setStatus(VideoProgressStatus.ASSISTIDO);
```

Constantes para paths repetidos (ex: `VIDEO_STREAM_PATH`).

## Persistencia

- **Proibido**: `save()` em loop
- **Obrigatorio**: `saveAll()` com colecao

```java
// ERRADO
for (Item item : items) {
    itemRepository.save(item);
}

// CORRETO
itemRepository.saveAll(items);
```

Queries com relacionamentos devem usar `JOIN FETCH` para evitar N+1.

## Validacao

- Todo `@RequestBody` em controller deve ter `@Valid`
- DTOs devem ter anotacoes Jakarta:
    - `@NotBlank` em nomes/titulos
    - `@NotNull` em IDs obrigatorios
    - `@Size` onde apropriado

```java
@PostMapping
public ResponseEntity<?> create(@Valid @RequestBody CreateSchoolRequest request) { ... }
```

## Autenticacao

Controllers devem usar `@AuthenticationPrincipal UsuarioAutenticado` para obter usuario logado.

```java
@GetMapping("/perfil")
public ResponseEntity<?> getPerfil(
    @AuthenticationPrincipal UsuarioAutenticado usuario) {
    ...
}
```

## Mapeamento DTO

- Usar metodo `toResponse()` estatico no record DTO ou mapper dedicado
- Nao converter manualmente em controllers

```java
public record SchoolResponse(UUID id, String name, ...) {
    public static SchoolResponse toResponse(School school) {
        return new SchoolResponse(school.getId(), school.getName(), ...);
    }
}
```

## Estrutura de Pacotes

```
com.example.claravalback/
├── app/util/              → utilitarios (EntityHelper, ChecksumUtil)
├── newversion/model/      → entidades JPA + Toggleable
├── newversion/model/enums → enums de status/tipo
├── newversion/service/    → regras de negocio (max 5 deps, max 250 linhas)
├── newversion/controller/ → endpoints REST (@Valid obrigatorio)
└── newversion/dto/        → records com validacao Jakarta
```

## Build e Testes

```bash
./mvnw clean package                  # Build completo
./mvnw clean package -DskipTests      # Build sem testes
./mvnw test                           # Rodar testes
```
