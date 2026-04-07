# Padrões Obrigatórios — Backend

Regras extraídas do `CLAUDE.md` do repositório [claraval-back](https://github.com/ZagoConsultoria/claraval-back).

## Limites de Tamanho

| Elemento | Limite |
|----------|--------|
| Dependências injetadas por service | Max 5 |
| Linhas por método | Max 40 |
| Linhas por arquivo de service | Max ~250 |

Se exceder dependências, decompor em services menores.

## Entity Lookup

- **Proibido**: `new EntityNotFoundException("string literal")`
- **Obrigatório**: `EntityHelper.findOrThrow(repo, id, "NomeEntidade")`

```java
// ERRADO
School school = schoolRepository.findById(id)
    .orElseThrow(() -> new EntityNotFoundException("Escola nao encontrada"));

// CORRETO
School school = EntityHelper.findOrThrow(schoolRepository, id, "School");
```

O `EntityHelper` está em `app/util/EntityHelper.java`.

## Toggle de Ativo

Entidades com campo `active` devem:

1. Implementar interface `Toggleable`
2. Usar `EntityHelper.toggleActive(repo, id, "NomeEntidade")`

Não reimplementar lógica de toggle manualmente.

## Exception Handling

- **Proibido**: `catch (Exception e)` genérico (exceto infraestrutura I/O justificada)
- **Obrigatório**: catch de exceções específicas

```java
// ERRADO
try { ... } catch (Exception e) { ... }

// CORRETO
try { ... } catch (EntityNotFoundException e) { ... }
try { ... } catch (IOException e) { ... }
```

## Strings e Enums

- **Proibido**: strings hardcoded para status (`"ASSISTIDO"`, `"EM_ANDAMENTO"`)
- **Obrigatório**: usar enums correspondentes

```java
// ERRADO
video.setStatus("ASSISTIDO");

// CORRETO
video.setStatus(VideoProgressStatus.ASSISTIDO);
```

Constantes para paths repetidos (ex: `VIDEO_STREAM_PATH`).

## Persistência

- **Proibido**: `save()` em loop
- **Obrigatório**: `saveAll()` com coleção

```java
// ERRADO
for (Item item : items) {
    itemRepository.save(item);
}

// CORRETO
itemRepository.saveAll(items);
```

Queries com relacionamentos devem usar `JOIN FETCH` para evitar N+1.

## Validação

- Todo `@RequestBody` em controller deve ter `@Valid`
- DTOs devem ter anotações Jakarta:
    - `@NotBlank` em nomes/títulos
    - `@NotNull` em IDs obrigatórios
    - `@Size` onde apropriado

```java
@PostMapping
public ResponseEntity<?> create(@Valid @RequestBody CreateSchoolRequest request) { ... }
```

## Autenticação

Controllers devem usar `@AuthenticationPrincipal UsuarioAutenticado` para obter usuário logado.

```java
@GetMapping("/perfil")
public ResponseEntity<?> getPerfil(
    @AuthenticationPrincipal UsuarioAutenticado usuario) {
    ...
}
```

## Mapeamento DTO

- Usar método `toResponse()` estático no record DTO ou mapper dedicado
- Não converter manualmente em controllers

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
├── app/util/              → utilitários (EntityHelper, ChecksumUtil)
├── newversion/model/      → entidades JPA + Toggleable
├── newversion/model/enums → enums de status/tipo
├── newversion/service/    → regras de negócio (max 5 deps, max 250 linhas)
├── newversion/controller/ → endpoints REST (@Valid obrigatório)
└── newversion/dto/        → records com validação Jakarta
```

## Build e Testes

```bash
./mvnw clean package                  # Build completo
./mvnw clean package -DskipTests      # Build sem testes
./mvnw test                           # Rodar testes
```
