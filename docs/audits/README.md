# Audits

**Status:** placeholder. No technical or security audit has been performed yet.

## Purpose

This directory will hold the outputs of the audits required by spec section 8, Phase 2: application
structure, dependencies, environment configuration, database schema and migrations, authentication
and RLS, the WhatsApp integration, API and MCP, automation and background processing, AI integration,
tests, and a prioritised technical risk register.

## What exists today

- The Phase 0 environment audit is a report, at `docs/reports/phase-0-environment-audit.md`.
- No codebase audit has been done. Nothing here should be read as an assessment of upstream quality
  or security.

## Rules

- Audit before modifying (spec section 12, principle 1).
- Mark each finding as verified, not verified, partially verified or blocked.
- Redact secrets. Never include real credentials or customer data.
