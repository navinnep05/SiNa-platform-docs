# JWT

## Purpose

Bearer token authentication for mobile sessions.

## Scope

Token issuance, validation, claims, and mobile storage.

## Decision

[ADR-0003](../decisions/ADR-0003-auth-v1-phase-1.md) — password login issues JWT; Phase 1b OTP/OAuth converge on same model ([ADR-0007](../decisions/ADR-0007-phase-1b-otp-and-google-oauth.md)).

## Backend

- Library: jjwt 0.12.6
- Sign with `JWT_SECRET` from environment
- Validate on every protected route via Spring Security filter
- Claims include role and account status — re-validated server-side

## Mobile

- Store token via `src/services/session.ts` (AsyncStorage)
- Send `Authorization: Bearer <token>` on API calls
- Session restore: `GET /api/v1/auth/me` on app launch — [AUTH_FLOW.md](../docs/architecture/AUTH_FLOW.md)
- Sign out clears stored token

## Policy (v1)

- Access token only — **no refresh token**
- Expired/invalid token → 401 → clear session → role selection
- Do not log tokens

## Related

- [SECURITY.md](../docs/architecture/SECURITY.md)
