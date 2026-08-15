# Commit Message Guide

## Purpose

Consistent commit messages that are easy to scan in history and PRs.

## Format

```
<type>: <short summary in imperative mood>

[optional body — what and why, not how line-by-line]
```

Summary: ≤ 72 characters, lowercase type prefix, no trailing period.

## Types

| Type | Use |
| --- | --- |
| `feat` | New user-visible behavior |
| `fix` | Bug fix |
| `docs` | Documentation only |
| `refactor` | Code change without behavior change |
| `test` | Tests only |
| `chore` | Tooling, deps, scaffold |
| `security` | Security fix or hardening |

Optional scope: `feat(booking): add broadcast timeout`

## Scope

Use module or repo area when helpful: `auth`, `booking`, `mobile-ui`, `openapi`.

Omit scope for small obvious changes.

## Examples

```
feat: add OTP verify endpoint for Phase 1b

docs: complete TESTING and DEPLOYMENT guides

fix(booking): reject accept when driver is unverified

test: cover booking routing exhaustion path

chore: bump springdoc to 3.0.3
```

## Do Not

- Vague messages: `fix stuff`, `updates`, `WIP`
- Mix unrelated changes in one commit
- Commit secrets, `.env`, or credentials
- Use `--no-verify` unless explicitly requested

Cross-repo features: separate commits per repo; reference the shared branch name in PR descriptions.

## Related

- [GIT_WORKFLOW.md](./GIT_WORKFLOW.md)
