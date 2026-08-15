# PostgreSQL

## Purpose

Primary relational datastore for runtime persistence.

## Scope

Schema design, migrations, indexing, and local development.

## Version

PostgreSQL **16** — `docker-compose.yml` image `postgres:16`.

## Migrations

- **Flyway** — SQL files under `src/main/resources/db/migration/`
- Naming: `V{version}__description.sql`
- Migrations run automatically on application startup
- Test profile uses H2 with compatible DDL where possible

## Design Reference

Canonical model: [DATABASE_DESIGN.md](../docs/architecture/DATABASE_DESIGN.md).

Key indexes for PRD journeys:

- `bookings(customer_id, status, requested_start_at)`
- `bookings(driver_id, status, requested_start_at)`
- `driver_profiles(status)`
- `notifications(user_id, read_at, created_at)`

## Local Setup

```bash
cd driver-booking-backend
docker compose up -d
```

Connection via `DB_*` env vars in `.env`.

## Related

- [DATABASE_ARCHITECT.md](../roles/DATABASE_ARCHITECT.md)
