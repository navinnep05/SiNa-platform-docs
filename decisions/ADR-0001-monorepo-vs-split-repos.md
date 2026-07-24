# ADR-0001: Monorepo vs Split Repos

## Status

Accepted

## Context

The Driver Booking platform needs separate backend and mobile codebases while preserving shared governance, standards, and architectural documentation.

## Decision

Use three repositories:

- `driver-booking-platform-docs` for shared governance and architecture
- `driver-booking-backend` for the Spring Boot backend
- `driver-booking-mobile` for the React Native app

## Consequences

- Shared standards remain centralized.
- Backend and mobile can evolve independently while following the same governance model.
- Repository-local `AGENTS.md` files must point back to the docs repository.

