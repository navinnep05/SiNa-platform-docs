# Coding Standards

## Purpose

Baseline expectations for code quality, readability, and maintainability.

## Scope

Backend (Java), mobile (TypeScript/React Native), and shared documentation.

## General Principles

- Match existing patterns in the file you are editing
- Prefer small, focused changes over drive-by refactors
- Keep business rules in services/domain — not in controllers or screen components
- One capability per class/function where practical

## Readability

- Use descriptive names over abbreviations
- Keep methods short; extract when nesting exceeds two levels
- Avoid commented-out code in merged branches
- Format with project defaults (Java: standard; mobile: ESLint + Prettier via RN config)

## Reuse

- Extract duplication only when used twice or more with the same semantics
- Do not create one-line utility wrappers
- Share booking/status logic via documented mappers — see [BOOKING_STATUS_MAPPING.md](../docs/architecture/BOOKING_STATUS_MAPPING.md)

## Layering

**Backend:** `api` → `service` → `repository` → `domain`. DTOs at the API boundary only.

**Mobile:** screens render; `src/state/flow.tsx` and `src/services/*` own behavior and API calls.

Cross-repo: no booking or verification business rules duplicated in mobile that are not also enforced on the backend.

## Testing

- Add tests for new service logic and state transitions
- Test failure paths — auth denied, invalid transitions, validation errors
- See [TESTING.md](../docs/delivery/TESTING.md)

## Documentation

- Update OpenAPI + mobile `api.ts` when changing contracts
- Update flow/ADR docs when behavior changes
- Update [docs/README.md](../docs/README.md) when adding docs

## Review Expectations

Every PR should be readable by a teammate without a walkthrough. If a change needs a diagram to explain, add it to the docs repo.

See [CODE_REVIEW_CHECKLIST.md](./CODE_REVIEW_CHECKLIST.md).
