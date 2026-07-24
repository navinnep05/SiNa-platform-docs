# Branching Strategy

## Purpose

Define the long-lived and short-lived branch model for the repository set.

## Scope

Applies to all backend, mobile, documentation, and release work.

## Table of Contents

- Long-Lived Branches
- Feature Branches
- Bugfix Branches
- Hotfix Branches
- Release Branches
- Naming Rules

## Long-Lived Branches

- `main` is the stable branch that tracks reviewed work.
- `develop` is not required for this setup and should only be introduced by team agreement.

## Feature Branches

- Use `feature/*` for normal feature work.
- When a feature touches backend and mobile, use matching branch names in both repos.
- When a feature touches docs plus an implementation repo, keep the docs branch name aligned with the implementation branch name.

## Bugfix Branches

- Use `bugfix/*` for non-urgent fixes.
- Keep bugfix branches narrow and easy to review.

## Hotfix Branches

- Use `hotfix/*` for urgent production fixes.
- Keep hotfix changes minimal and well documented.

## Release Branches

- Use `release/*` for stabilization and release prep.
- Only create release branches when the team needs a formal freeze window.

## Naming Rules

- Prefer lowercase branch names with hyphens.
- Keep the branch name readable and tied to the business feature.
- Avoid repo-specific names inside the branch name unless the work is repo-specific.

## Future Implementation Notes

- Clarify branch lifetime and merge sequence when CI is in place.
