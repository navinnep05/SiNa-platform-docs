# Notifications

## Purpose

Notification delivery across push and in-app inbox.

## Scope

Event triggers, templates, backend module, and mobile inbox UI.

## Architecture

- **Notification domain module** (backend) owns delivery history and inbox state
- **Firebase** delivers push to device — [FIREBASE.md](./FIREBASE.md)
- Chat new-message awareness via push; message body fetched via REST polling ([ADR-0005](../decisions/ADR-0005-chat-transport-v1-rest-polling.md))

## Event Examples

| Event | Push | In-app inbox |
| --- | --- | --- |
| Booking request to driver | Yes | Yes |
| Booking accepted | Yes | Yes |
| Verification approved/rejected | Yes | Yes |
| Booking expired | Yes | Yes |
| New chat message | Yes | Via chat poll |

## Mobile

- `src/notifications/` — inbox list and read state
- Deep links to relevant screen where implemented

## Backend

- Persist notification records per user
- Idempotent delivery where retry occurs
- Do not embed secrets or full PII in push payload title/body

## Related

- [SYSTEM_ARCHITECTURE.md](../docs/architecture/SYSTEM_ARCHITECTURE.md)
