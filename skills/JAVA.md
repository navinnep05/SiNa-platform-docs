# Java

## Purpose

Language baseline for backend development.

## Scope

Java 21 features, package layout, and testability conventions.

## Version

**Java 21** (LTS) — pinned in `pom.xml` `<java.version>`.

## Conventions

- Use records for immutable DTOs where appropriate (`ApiErrorResponse`)
- Prefer constructor injection (Lombok `@RequiredArgsConstructor` on services)
- Keep entities in `domain` packages — never return from controllers
- Use `Optional` at repository boundaries; avoid propagating null through services
- MapStruct for entity ↔ DTO mapping

## Testing

- JUnit 5 + Mockito / Spring test slices
- `@WebMvcTest` for controllers; full context only when integration requires it
- Test modules mirror `src/main/java/.../modules/<domain>/`

## Related

- [SPRING_BOOT.md](./SPRING_BOOT.md)
- [CODING_STANDARDS.md](../standards/CODING_STANDARDS.md)
