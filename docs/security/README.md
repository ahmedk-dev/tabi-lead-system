# Security

**Status:** placeholder. No security review has been performed on the codebase.

## Binding requirements

Spec sections 6.4 and 7 govern. In summary:

- Never commit `.env*` files (other than upstream `*.example` templates), Supabase service-role
  keys, Meta application secrets, access tokens, encryption keys or production credentials.
- Use synthetic data only. Do not connect a real customer's WhatsApp number before the integration
  is tested and reviewed.
- Enforce permissions on the server and in the database, not only in the UI.
- Do not assume the existing account-level Row Level Security gives complete multi-tenant isolation.
  It must be verified and tested.
- Document any serious weakness here or in the relevant phase report.

## What exists today

- Upstream publishes its own vulnerability-reporting policy at `.github/SECURITY.md`. That policy
  is for upstream's repository. It has not been adapted for the Tabi fork. **Decision needed:** who
  receives security reports for this fork.
- No Tabi security findings have been recorded yet. The security audit belongs to Phase 2.

## Findings register

None recorded.
