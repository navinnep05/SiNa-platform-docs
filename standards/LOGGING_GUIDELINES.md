# Logging Guidelines

## Purpose

Consistent logging for diagnostics, support, and security auditing.

## Scope

Backend services (primary). Mobile: debug logs in dev only; no sensitive data in production logs.

## Log Levels

| Level | Use |
| --- | --- |
| ERROR | Unhandled failures, data corruption risk, external dependency down |
| WARN | Handled domain failures, rate limits, retryable dependency errors |
| INFO | Startup, migration success, major business events (booking accepted) |
| DEBUG | Request flow detail — dev/local only |
| TRACE | Avoid in production |

## Structure

- Prefer structured key-value logs where the backend logging stack supports it
- Include: `traceId`, `userId` (if authenticated), `bookingId` / entity ID when relevant
- Use consistent event names: `booking.accepted`, `verification.approved`

## Sensitive Data

**Never log:** passwords, OTP codes, JWT tokens, DL/RC document content, full phone numbers in production.

Mask identifiers in INFO logs when possible (e.g. last 4 digits of mobile).

## Correlation

- Generate/propagate `traceId` per request — returned in `ApiErrorResponse`
- Mobile may send a client request ID header in future; backend traceId is canonical for support today

## Error Logging

- Log stack traces at ERROR for unexpected exceptions
- Log handled domain failures at WARN with `errorCode`, not full stack
- Do not double-log the same exception at ERROR and WARN

## Audit Logging

Record at INFO (or dedicated audit sink later):

- Admin verification approve/reject with reason
- Booking state transitions with actor role
- Account registration and OAuth link events

Retention policy TBD — keep audit fields in DB even when soft-deleting entities ([DATABASE_DESIGN.md](../docs/architecture/DATABASE_DESIGN.md)).

## Related

- [SECURITY.md](../docs/architecture/SECURITY.md)
