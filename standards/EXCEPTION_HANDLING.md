# Exception Handling

## Purpose

Define how errors are raised, translated, and returned.

## Scope

Backend domain errors, validation, and API responses. Mobile error display follows backend codes.

## Principles

- Fail with explicit domain exceptions — do not return null for error cases
- Map all handled exceptions in `GlobalExceptionHandler` — one HTTP status per exception type
- Use stable `errorCode` strings consumed by mobile
- Include `traceId` on every API error response

## Domain Errors

Throw typed exceptions from services:

| Exception | HTTP | Example codes |
| --- | --- | --- |
| `ValidationException` | 400 | `INVALID_INPUT` |
| `InvalidStateTransitionException` | 409 | booking transition violations |
| `ConflictException` | 409 | duplicate resource |
| `ForbiddenOperationException` | 403 | unverified driver action |
| `NotFoundException` | 404 | missing booking/vehicle |
| `RateLimitExceededException` | 429 | OTP throttling |

Keep messages user-safe — no stack traces in responses.

## Validation Errors

- Bean validation → `VALIDATION_ERROR` with `fieldErrors` list
- One message per field in `FieldViolationResponse`

## System Errors

- Uncaught exceptions → `500` with generic message; log full stack server-side only
- Do not expose internal class names or SQL in API responses

## API Mapping

Implementation: `com.driverbooking.backend.common.error.GlobalExceptionHandler`.

Mobile: map `errorCode` in `src/auth/formatApiError.ts` for user-facing copy.

## Recovery Guidance

| Error | Client action |
| --- | --- |
| 401 | Clear session; return to auth |
| 409 booking | Refresh booking state from server |
| 429 OTP | Show wait/retry message |
| 500 | Retry once; then show generic failure |

Retriable: transient network errors. Non-retriable: validation, auth, state conflicts.

## Related

- [API_STANDARDS.md](./API_STANDARDS.md)
