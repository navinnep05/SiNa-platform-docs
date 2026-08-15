# Clean Architecture

## Purpose

Layering and dependency rules for maintainable modules.

## Scope

Backend modular monolith; mobile screen/service separation.

## Backend Layers

```
API (controllers, DTOs)
  ↓
Service (use cases, transactions)
  ↓
Repository (persistence)
  ↓
Domain (entities, enums, domain rules)
```

Rules:

- Dependencies point inward — domain does not depend on API
- Cross-module calls go through service interfaces, not repositories
- Shared kernel limited to `common` and `shared` packages

## Mobile Layers

```
Screens (UI, user events)
  ↓
State / hooks (flow.tsx, React Query)
  ↓
Services (api.ts, session.ts)
```

Rules:

- Screens do not call Axios directly — use services/state
- Backend re-validates all authorization and booking rules

## Module Boundaries

Per [ADR-0002](../decisions/ADR-0002-modular-monolith-phase-1.md):

- identity/auth ≠ booking ≠ verification ≠ notifications
- Extraction to separate services later requires ADR update

## Related

- [SYSTEM_ARCHITECTURE.md](../docs/architecture/SYSTEM_ARCHITECTURE.md)
- [CODING_STANDARDS.md](../standards/CODING_STANDARDS.md)
