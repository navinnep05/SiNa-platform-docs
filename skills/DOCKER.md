# Docker

## Purpose

Container support for backend runtime and local PostgreSQL.

## Scope

Dockerfile, compose, and deployment artifacts.

## Local Database

`driver-booking-backend/docker-compose.yml`:

```bash
docker compose up -d
```

PostgreSQL 16 on port 5432, database `driver_booking`.

## Backend Image

Multi-stage `Dockerfile`:

1. Build: `maven:3.9.9-eclipse-temurin-21` → `./mvnw package`
2. Run: `eclipse-temurin:21-jre` → port 8080

```bash
docker build -t driver-booking-backend:local .
docker run --env-file .env -p 8080:8080 driver-booking-backend:local
```

## Notes

- Pass all secrets via `--env-file` or orchestrator secrets — not baked into image
- Mobile is not containerized in Phase 1 — APK build on developer CI/machine

## Related

- [DEPLOYMENT.md](../docs/delivery/DEPLOYMENT.md)
