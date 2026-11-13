# Deployment

**Status:** placeholder. Nothing has been deployed and no deployment has been configured.

## Policy (from the spec)

- Spec section 3.3: Docker is not a prerequisite for initial development. Initial development uses
  Node.js, the project's package manager scripts, a dedicated Supabase cloud development project
  and the local Next.js dev server.
- Spec section 9.4: no deployment to production without explicit approval.
- Production deployment, monitoring, backups and customer onboarding belong to Phase 8.

## What exists today

- Upstream ships a `Dockerfile`, `docker-compose.yml` and `docs/docker.md`, and its README recommends
  a third-party host. These are upstream materials. They have **not** been tested or adopted for Tabi.
- Docker is not installed on the development machine (Phase 0 report).
- No Supabase project, hosting account or domain exists for this project.
- Upstream branding and URLs have not been replaced (see `README.md`, Licence and attribution).

## Rules

- Do not deploy, create cloud resources or touch production credentials without owner approval.
- Document each deployment procedure here only after it has been performed and verified.
