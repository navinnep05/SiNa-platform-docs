# API Standards

## Purpose

Define API design rules for consistency, stability, and security.

## Scope

Backend endpoints, DTOs, error contracts, and mobile client integration.

## Resource Design

- Base path: `/api/v1/**`
- Use nouns for resources; verbs only for non-CRUD actions (`/auth/login`, `/bookings/{id}/accept`)
- Group by domain tag: Authentication, Driver, Customer, Vehicle, Booking, Notification, Admin
- Controllers return DTOs — never expose JPA entities
- Keep module boundaries: auth does not own booking logic ([SYSTEM_ARCHITECTURE.md](../docs/architecture/SYSTEM_ARCHITECTURE.md))

Canonical contract: [docs/api/openapi.yaml](../docs/api/openapi.yaml).

## Validation

- Use Jakarta Validation annotations on request DTOs
- Fail fast with `400` and field-level violations
- Domain rules (e.g. invalid booking transition) throw domain exceptions mapped by `GlobalExceptionHandler`

## Errors

Standard envelope (`ApiErrorResponse`):

```json
{
  "errorCode": "VALIDATION_ERROR",
  "message": "Request validation failed",
  "traceId": "uuid",
  "timestamp": "2026-08-13T16:00:00Z",
  "fieldErrors": [
    { "field": "email", "message": "must not be blank" }
  ]
}
```

HTTP mapping:

| Status | When |
| --- | --- |
| 400 | Validation, malformed input |
| 401 | Missing/invalid JWT |
| 403 | Authenticated but not permitted |
| 404 | Resource not found |
| 409 | Invalid state transition, conflict |
| 429 | Rate limit (OTP, etc.) |
| 500 | Unexpected server error |

Use stable `errorCode` strings — mobile maps them in `formatApiError.ts`.

## Pagination

Phase 1 list endpoints return bounded lists without cursor pagination unless volume requires it. When adding pagination:

- Use `page`, `size`, `total` in a consistent wrapper
- Document in OpenAPI before mobile adoption

## Security

- Protected routes require `Authorization: Bearer <token>`
- Public routes: register, login, OTP request/verify, OAuth (Phase 1b)
- Enforce role and resource ownership in the service layer
- Do not put PII or secrets in URL paths or query strings

## Versioning

- `/api/v1` is the current version
- Additive changes (new optional fields, new endpoints) do not require a version bump
- Breaking changes require `/solution-architect` sign-off and coordinated mobile update

## Observability

- Every error response includes a `traceId`
- Log server-side with the same trace ID at WARN/ERROR for failures
- Do not log request bodies containing passwords, OTP, or tokens

## Related

- [api/README.md](../docs/api/README.md)
- [EXCEPTION_HANDLING.md](./EXCEPTION_HANDLING.md)
