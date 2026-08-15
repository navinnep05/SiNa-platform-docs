# Spring Boot

## Purpose

Backend application framework for the Driver Booking modular monolith.

## Scope

Bootstrap, configuration, web layer, dependency injection, and module layout.

## Application Structure

```
com.driverbooking.backend
├── config/          # Security, JWT, OTP delivery, OpenAPI
├── common/          # errors, shared utilities
└── modules/
    └── <domain>/
        ├── api/         # controllers + DTOs
        ├── service/
        ├── repository/
        └── domain/      # entities, enums
```

**Active modules:** authentication, admin, booking, customer, driver, notification, vehicle.

Single deployable JAR — [ADR-0002](../decisions/ADR-0002-modular-monolith-phase-1.md).

## Configuration

- **Profiles:** `local` (default), `dev`, `prod` — `application-{profile}.properties`
- **Base:** `application.properties` — shared defaults (JWT, OTP TTL, Google OAuth client ID)
- **Secrets:** environment variables — see backend `.env.example`
- **Default profile:** `spring.profiles.default=local` for `./mvnw spring-boot:run` on a laptop

Override profile: `SPRING_PROFILES_ACTIVE=dev`.

## Phase 1b auth (live — ADR-0007)

OTP and Google OAuth ship **enabled** in code — not behind feature flags.

### OTP delivery by profile

| Profile | `auth.otp.delivery` | Behavior |
| --- | --- | --- |
| `local` | `console` | OTP codes logged to server console (`auth.otp.dev-log-codes=true`) |
| `dev` | `sms` | `StubSmsVendorAdapter` — codes logged until real vendor wired |
| `prod` | `sms` | Real vendor required — startup fails if `vendor=stub` |

Key properties (`auth.otp.*`):

- `enabled`, `ttl`, `max-attempts`, `resend-cooldown`
- SMS vendor: `auth.otp.sms.vendor`, `api-key`, `sender-id`, `log-codes-in-stub`

Adapters wired in `OtpDeliveryConfig` via `@ConditionalOnProperty` — `ConsoleOtpDeliveryAdapter`, `SmsOtpDeliveryAdapter` + `SmsVendorPort`.

### Google OAuth

| Property | Purpose |
| --- | --- |
| `auth.oauth.google.enabled` | Kill switch (default `true`) |
| `auth.oauth.google.client-id` | Web client ID — must match mobile `GOOGLE_WEB_CLIENT_ID` |

`OAuthService` + `GoogleIdTokenVerifierAdapter` validate idTokens server-side. Tests use `StubGoogleTokenVerifier`.

Endpoints (both roles, same API):

- `POST /api/v1/auth/otp/request`
- `POST /api/v1/auth/otp/verify`
- `POST /api/v1/auth/oauth/google`

Detail: [AUTH_FLOW.md](../docs/architecture/AUTH_FLOW.md).

## Web Layer

- REST controllers under `/api/v1/**`
- Jakarta Validation on request DTOs
- `GlobalExceptionHandler` for error envelope — [API_STANDARDS.md](../standards/API_STANDARDS.md)
- springdoc OpenAPI at runtime; export to [docs/api/openapi.yaml](../docs/api/openapi.yaml)

## Commands

```bash
./mvnw spring-boot:run
./mvnw test
./mvnw clean verify
```

Local DB: `docker compose up -d` in `driver-booking-backend` — [DOCKER.md](./DOCKER.md).

## Related

- [TECH_STACK.md](../docs/architecture/TECH_STACK.md)
- [JAVA.md](./JAVA.md)
- [JWT.md](./JWT.md)
- [DEPLOYMENT.md](../docs/delivery/DEPLOYMENT.md)
