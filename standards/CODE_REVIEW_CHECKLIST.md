# Code Review Checklist

## Purpose

Consistent checklist for reviewing changes across the platform repos.

## Correctness

- [ ] Logic matches PRD / flow doc / ADR for the feature
- [ ] Edge cases handled (empty input, not found, concurrent updates)
- [ ] Booking state transitions match [BOOKING_STATUS_MAPPING.md](../docs/architecture/BOOKING_STATUS_MAPPING.md)
- [ ] No silent failures — errors surfaced to caller/user

## Architecture

- [ ] Change respects module boundaries ([ADR-0002](../decisions/ADR-0002-modular-monolith-phase-1.md))
- [ ] No business rules only in mobile that backend should enforce
- [ ] Cross-repo contract changes have docs/OpenAPI update in same delivery wave
- [ ] Escalated to `/solution-architect` if boundary or breaking contract

## Security

- [ ] AuthZ checks on protected resources
- [ ] No secrets, tokens, or OTP in logs or committed files
- [ ] Input validated at API boundary
- [ ] Document upload paths respect [ADR-0004](../decisions/ADR-0004-document-storage-v1.md)

## Testing

- [ ] New service logic has unit tests
- [ ] Failure paths tested (401, 403, 409, validation)
- [ ] `./mvnw verify` or `npm test` passes locally
- [ ] Manual smoke noted in PR if automation gaps exist

## Documentation

- [ ] OpenAPI + mobile `api.ts` updated if API changed
- [ ] Flow/ADR/docs updated if behavior changed
- [ ] [docs/README.md](../docs/README.md) updated if new doc added

## Maintainability

- [ ] Naming follows [NAMING_CONVENTIONS.md](./NAMING_CONVENTIONS.md)
- [ ] No unnecessary abstraction or duplicate logic
- [ ] Readable without author present

## Release Risk

- [ ] Flyway migration backward-safe or rollback plan noted
- [ ] Mobile build compatible with deployed backend version
- [ ] Feature flags for incomplete Phase 1b paths if merging incrementally

## Related

- [CODING_STANDARDS.md](./CODING_STANDARDS.md)
- [GIT_WORKFLOW.md](./GIT_WORKFLOW.md)
