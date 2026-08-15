# Naming Conventions

## Purpose

Define naming rules for code, files, packages, branches, and documentation.

## Scope

Applies to backend, mobile, documentation, git branches, and shared artifacts.

## Table of Contents

- Packages
- Classes
- Methods
- Variables
- Files
- Branches
- Documents

## Placeholder Sections

### Packages

Placeholder guidance for package naming.

### Classes

Placeholder guidance for type naming.

### Methods

Placeholder guidance for behavior-oriented method names.

### Variables

Placeholder guidance for variable naming clarity.

### Files

Placeholder guidance for file and folder naming.

### Branches

Placeholder guidance for git branch naming.

### Documents

**Folder placement under `docs/`:**

| Folder | Put here |
| --- | --- |
| `product/` | PRD, user flows, readiness checklists |
| `architecture/` | System design, stack, auth, database, security, status mappings |
| `design/` | UI/UX guidelines |
| `delivery/` | Testing, deployment, release |
| `delivery/implementation/` | One `PHASE-*-IMPLEMENTATION.md` per delivery phase |
| `api/` | OpenAPI contract only |

**Naming:**

| Kind | Convention | Example |
| --- | --- | --- |
| Shared docs | `UPPER_SNAKE_CASE.md` | `BOOKING_FLOW.md` |
| PRD | `PRD-####-kebab-title.md` | `PRD-0001-driver-hiring-application.md` |
| ADR | `ADR-####-kebab-title.md` | `ADR-0002-modular-monolith-phase-1.md` |
| PDR | `PDR-####-kebab-title.md` | `PDR-0001-broadcast-matching-phase-1.md` |
| Phase implementation | `PHASE-#-IMPLEMENTATION.md` | `PHASE-1B-IMPLEMENTATION.md` |

- One canonical doc per topic — link, don't duplicate.
- Update [docs/README.md](../docs/README.md) and the folder README when adding or renaming.
- Mark status: Complete, Partial, or Placeholder in the index.

## Future Implementation Notes

- Add examples for backend and mobile naming patterns.

