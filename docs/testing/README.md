# Testing

**Status:** placeholder. No checks have been run in this repository.

## Purpose

This directory will hold test plans, results and evidence: baseline check results (Phase 3),
functional test reports (Phase 4), WhatsApp integration evidence (Phase 5), and later the
automated tenant-isolation tests required by spec section 6.4.

## Commands defined by upstream

From `package.json` at the baseline commit (read from the file, **not yet executed here**):

| Command | Script |
|---|---|
| `npm run lint` | `eslint` |
| `npm run typecheck` | `tsc --noEmit` |
| `npm test` | `vitest run` |
| `npm run build` | `next build` |

`package.json` requires Node `>=22.12.0`. The test files present in the tree were counted but not
run. Dependencies are not installed, so none of these commands has been tried.

## Rules

- Never claim success without evidence. Record the exact command and its result.
- Use synthetic contacts and conversations only.
- Cross-tenant access tests are required before any multi-tenant release.
