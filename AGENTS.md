<!-- BEGIN:nextjs-agent-rules -->
# This is NOT the Next.js you know

This version has breaking changes — APIs, conventions, and file structure may all differ from your training data. Read the relevant guide in `node_modules/next/dist/docs/` before writing any code. Heed deprecation notices.
<!-- END:nextjs-agent-rules -->

<!-- BEGIN:tabi-agent-rules -->
# Tabi Lead System — Agent Instructions

These instructions are specific to this repository (the Tabi-owned fork of
[ArnasDon/wacrm](https://github.com/ArnasDon/wacrm)). The block above is upstream's and is
kept unchanged. Everything between the `tabi-agent-rules` markers is Tabi's. Read both
before doing any work.

## 1. Product vision and scope

Tabi Lead System (working name) is intended to become a self-hostable WhatsApp and
multi-channel lead-management platform owned by Tabi Digital. It starts from the wacrm
codebase and is adapted in controlled phases. The long-term goal is a secure multi-tenant
SaaS, with separate per-customer installations as an acceptable intermediate step.

Today this repository is the **unmodified upstream wacrm application plus Tabi project
documentation**. Do not describe or document planned features as if they already exist.

## 2. Governing documents and hierarchy

1. `docs/resources/tabi-lead-system-spec-doc.md` is the governing specification.
   Do not edit, move, rename, duplicate or "tidy" it. Changes require explicit approval from the project owner.
2. This `AGENTS.md`.
3. The current phase prompt from the project owner or reviewer.
4. Reports in `docs/reports/` (the record of what was done and verified).
5. Area READMEs: `docs/architecture/`, `docs/audits/`, `docs/testing/`, `docs/security/`, `docs/deployment/`.
6. Upstream documentation (`README.md` upstream section, `docs/*.md` such as `public-api.md`, `mcp.md`, `docker.md`)
   describes upstream behaviour. Verify it against the code before relying on it.

If sources conflict, the higher item wins. Report the conflict rather than resolving it silently.

## 3. Phased development

Work proceeds in the phases defined in spec section 8 (Phase 0 environment audit through Phase 9 commercial capabilities).

- Do only what the current phase prompt authorises.
- **Stop at the end of every assigned phase or task and wait for explicit approval.** Never start the next phase.
- Phases completed so far are listed in `docs/reports/`.
- Do not implement features from later phases early, even when they look easy.

## 4. Inspect before modifying

- Read the relevant code, migrations and documentation before proposing or making changes.
- Verify versions, commands, file paths and behaviour from the repository. Do not rely on memory or on upstream prose.
- Do not assume this is the Next.js you know (see the upstream block above). `node_modules/` is not installed by default; installing dependencies is a Phase 3 task unless a prompt says otherwise.
- Do not change the technology stack without a documented justification and approval.

## 5. Security and tenant isolation

Security is a core requirement, not a final polish step. Spec sections 6.4 and 7 are binding.

- Never commit `.env*` files (other than the upstream `*.example` templates), Supabase service-role keys, Meta app secrets,
  access tokens, encryption keys or any production credential.
- Never print secrets in reports, logs or terminal summaries. Redact them.
- Use synthetic contacts and conversations only. Do not connect a real customer's WhatsApp number before the
  integration is tested and reviewed.
- Do not assume the existing account-scoped Row Level Security gives complete multi-tenant isolation. It must be
  verified and tested before any SaaS use.
- Permissions must be enforced on the server and in the database, not only hidden in the UI.
- Record serious weaknesses in `docs/security/` or in the phase report. Do not leave them undocumented.

## 6. Testing and verification

- Run the relevant checks after a change. The upstream `package.json` defines: `npm run lint`, `npm run typecheck`,
  `npm test` (vitest) and `npm run build`. Their results have **not yet been verified in this repository**.
- Never claim success without evidence. State exactly which command ran and what it returned.
- Distinguish: Implemented and verified / Implemented but not verified / Partially implemented / Not implemented / Blocked.
- Tests that attempt cross-tenant access are required before any multi-tenant release (spec section 6.4).

## 7. Reporting

Every task ends with one report in `docs/reports/`, as specified in spec section 9.3: date, phase and task,
objective, work completed, files changed, commands executed, tests and results, outstanding issues, risks,
decisions required, recommended next step, and Git branch and commit where applicable. Keep reports factual
and mark each claim as verified, not verified, partially verified or blocked.

## 8. Prohibited actions and approval boundaries

Do not do any of the following without explicit approval from the project owner:

- Push to `upstream`, rewrite published history, force-push, or delete branches or tags.
- Deploy anywhere, or touch production systems or credentials.
- Create or modify cloud resources (for example Supabase projects) unless the current phase says so.
- Delete or rewrite existing migrations or project data.
- Change global Git configuration, system configuration or unrelated projects.
- Install or remove system software.
- Edit anything under `.commandcode/taste/` by hand.
- Change licensing, attribution or the `LICENSE` file.

Decisions that need the owner: architecture changes, product direction, new external services, credentials,
production deployment, and anything the spec marks as requiring review.

## 9. Git workflow

- `origin` is the Tabi fork (`https://github.com/ahmedk-dev/tabi-lead-system`). `upstream` is `https://github.com/ArnasDon/wacrm`. Use HTTPS.
- Use repository-local Git configuration only. The recorded author is `Ahmed <amed.kivumbi@gmail.com>`.
- `main` is the integration branch. Do implementation work on a focused branch and keep commits small with descriptive messages.
- The baseline tag is `tabi-baseline-0.1.0`.
- `.commandcode/settings.json` is machine-local (it accumulates shell permissions) and is excluded through
  `.git/info/exclude`. It is not committed.

## 10. Working with upstream

- Treat upstream history as read-only. Never push to `upstream`.
- Keep Tabi changes isolated and minimal in upstream-owned files to ease future merges.
  Prefer new files and clearly delimited blocks. This file and `README.md` are already shared with upstream, so keep Tabi
  content inside the marked sections.
- To review upstream changes: `git fetch upstream`, then inspect `git log main..upstream/main` and the diff.
  Do not merge without a documented review of migrations, dependencies and security fixes.
- Upstream migrations are numbered `001`–`059` with gaps. Check for conflicts before adding Tabi migrations.
  Never renumber or edit an existing migration.
- Record every upstream integration in `docs/reports/` with the upstream commit range.

## 11. Licence and attribution

The upstream code is MIT-licensed (`LICENSE`, Copyright (c) 2026 Arnas Donauskas). The licence and copyright notice
must stay in the repository. Upstream asks public forks to replace its name, favicon and `wacrm.tech` URL with their own
before putting a deployment in front of users. That rebranding is not yet done and belongs to a later phase.
<!-- END:tabi-agent-rules -->
