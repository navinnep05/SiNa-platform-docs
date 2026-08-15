# TypeScript

## Purpose

Language baseline for the mobile client.

## Scope

Typing conventions, API interfaces, and test files.

## Conventions

- Strict typing for API payloads — mirror [openapi.yaml](../docs/api/openapi.yaml) in `src/services/api.ts`
- Prefer `interface` for DTO shapes; `type` for unions (booking display states)
- Avoid `any` — use `unknown` + narrowing for error payloads
- Colocate tests as `__tests__/*.test.ts(x)`

## API Types

Phase 1 uses **manual** TypeScript interfaces (no OpenAPI codegen). When the contract changes:

1. Update backend + regenerate OpenAPI
2. Update `api.ts` interfaces
3. Update `flow.tsx` mappers if enums changed

## Env Types

`src/types/env.d.ts` for build-time env vars — see `src/config/env.ts`.

## Related

- [REACT_NATIVE.md](./REACT_NATIVE.md)
- [api/README.md](../docs/api/README.md)
