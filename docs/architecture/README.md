# Architecture

**Status:** placeholder. No Tabi architecture documentation exists yet.

## Purpose

This directory will hold architecture documentation for Tabi Lead System: system overview,
database design and architecture decision records. The proposed layout is in spec section 10
(`docs/resources/tabi-lead-system-spec-doc.md`).

## What exists today

- The application is the unmodified upstream wacrm code. Its structure has been listed but **not
  audited**. The architecture audit belongs to Phase 2 (spec section 8).
- Upstream describes its own architecture on its website. That is not copied here and has not
  been verified.

## Rules

- Document only what has been verified from the code, migrations or running system.
- Architecture changes, and in particular the multi-tenant design (spec section 6 and Phase 7),
  need project-owner approval before implementation.
- Record each significant decision as a separate file under `docs/architecture/decisions/`
  (to be created when the first decision is recorded).
