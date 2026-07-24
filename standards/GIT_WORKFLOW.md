# Git Workflow

## Purpose

Define how work moves through branches, commits, and reviews.

## Scope

Applies to the three-repo Driver Booking platform setup:

- `driver-booking-platform-docs`
- `driver-booking-backend`
- `driver-booking-mobile`

## Table of Contents

- Branch Types
- Feature Flow
- Commit Discipline
- Merge Expectations
- Documentation Updates

## Branch Types

- `main` for stable, reviewed work
- `develop` only if the team explicitly adopts it later
- `feature/*` for normal feature work
- `bugfix/*` for fixes that are not urgent production issues
- `hotfix/*` for urgent production fixes
- `release/*` for stabilization work

## Feature Flow

- Use the docs repo first when a change affects governance, requirements, flows, or architecture.
- Use backend and mobile repos for implementation work.
- For a cross-cutting feature, use matching branch names across backend and mobile, for example `feature/booking-cancellation`.
- Keep branch names short, readable, and shared across the repos that participate in the same feature.

## Commit Discipline

- Make small, focused commits.
- Keep commits scoped to a single repo whenever possible.
- Use conventional, readable messages such as `chore: initial backend scaffold`.
- Do not mix docs-only changes with unrelated implementation work unless they are part of the same feature decision.

## Merge Expectations

- Open a separate PR per repo when a feature touches more than one repository.
- Merge docs changes first when they define the behavior, then backend, then mobile when sequencing matters.
- Avoid merging partial feature slices unless the receiving repo can stay in a clean, buildable state.

## Documentation Updates

- Update the docs repo whenever requirements, flows, architecture decisions, or repo boundaries change.
- Record notable delivery progress in `execution-log/`.
- Record irreversible architectural choices in `decisions/`.
- Keep repo-local `AGENTS.md` files pointing back to the docs repo as the source of truth.

## Future Implementation Notes

- Add examples for a backend/mobile coordinated feature branch pair.
