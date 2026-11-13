# Tabi Lead System — Project Specification

**Document type:** Product and technical implementation specification  
**Project name:** Tabi Lead System (working name)  
**Starting codebase:** [wacrm](https://github.com/ArnasDon/wacrm)  
**Implementation agent:** Command Code, initially DeepSeek V4.1 Flash; Sonnet 5.5 preferred for implementation where affordable  
**Technical reviewer and project coordinator:** ChatGPT  
**Project status:** Pre-implementation  
**Initial development environment:** Linux Mint, Node.js, local development server and hosted Supabase development project

---

## 1. Project overview

### 1.1 Purpose

Build a self-hostable WhatsApp and multi-channel lead management platform, starting from the open-source wacrm codebase and progressively adapting it into a product owned and controlled by Tabi Digital.

The resulting product should help businesses capture, organise, respond to, qualify and convert enquiries into customers.

It must go beyond being a WhatsApp chatbot or a rebranded copy of wacrm. The objective is to develop a flexible lead-management system that can eventually be offered to multiple businesses as a commercial SaaS product.

### 1.2 Product vision

A central workspace where a business can manage incoming enquiries, communicate with prospects, track sales opportunities, automate follow-ups and understand how its marketing generates leads.

The product should eventually support multiple businesses, each with its own team, contacts, conversations, sales processes, integrations, configuration and data.

### 1.3 Working product name

**Tabi Lead System**

This is a provisional internal name. Naming, branding and public positioning can be finalised separately.

---

## 2. Product objectives

The project should achieve the following objectives:

1. Establish a reliable, self-hostable foundation using an existing open-source CRM.
2. Provide a shared WhatsApp inbox that supports multiple team members.
3. Manage leads and contacts independently of individual conversations.
4. Track prospects through configurable sales pipelines.
5. Capture enquiries from websites and other digital channels.
6. Support structured lead qualification and follow-up management.
7. Automate routine lead-management activities.
8. Introduce AI assistance where it provides practical business value.
9. Provide useful reporting and lead-conversion analytics.
10. Evolve towards a secure multi-tenant SaaS platform.
11. Preserve the ability to deploy individual customer installations where appropriate.
12. Maintain ownership of the custom code, product direction and customer experience.

---

## 3. Starting point and technology

### 3.1 Base code

Use the public repository:

https://github.com/ArnasDon/wacrm

The repository is the starting foundation, not the final product specification.

The implementation agent must inspect the actual repository before making assumptions about its architecture, capabilities, dependencies, database structure or security.

### 3.2 Expected technology stack

The repository currently describes a stack based on:

- Next.js and React
- TypeScript
- Tailwind CSS
- Supabase
- PostgreSQL
- Supabase Authentication, Storage and Realtime
- Official Meta WhatsApp Business Cloud API
- Optional AI integrations
- REST API
- Model Context Protocol (MCP) server

The agent must verify the current versions and implementation details during the initial audit.

Do not replace the existing technology stack without a documented technical justification and approval.

### 3.3 Docker policy

Docker is **not a prerequisite for initial development**.

Initial development will use:

- Node.js installed on the development machine.
- The project's normal package manager and scripts.
- A dedicated Supabase cloud development project.
- The local Next.js development server.

Docker may be introduced later to:

- Run Supabase locally.
- Test the product's self-hosting capabilities.
- Reproduce production-like infrastructure.
- Validate container-based deployment.

Do not install or configure Docker as part of the initial setup unless the repository audit establishes a specific requirement.

### 3.4 Development environment

The initial development environment is:

- Operating system: Linux Mint XFCE.
- Hardware: Dell Latitude 7420.
- Node.js: v24.19.0.
- npm: 11.17.0.
- Git: 2.43.0.
- Existing project workspaces should remain separate from Tabi Digital's Astro website.

Proposed local project directory:

`~/projects/tabi-lead-system`

The agent must first inspect the machine and confirm its actual state. Do not assume every listed tool or version remains unchanged.

---

## 4. Product functionality

The following capabilities define the intended product direction. They are not all required in the first release.

### 4.1 Shared inbox and conversations

- Centralised WhatsApp conversation inbox.
- Multiple team members working from one business number.
- Conversation assignment.
- Conversation status and internal notes.
- Contact details accessible from conversations.
- Message delivery and read status where supported.
- Human handoff from automated responses.
- Conversation search and filtering.

### 4.2 Contact and lead management

- Central contact database.
- Contact profiles.
- Contact tags and categories.
- Custom fields.
- Contact import and deduplication.
- Lead source attribution.
- Contact activity history.
- Notes and interaction history.
- Lead qualification information.

The system must eventually distinguish between a contact, a lead, a conversation and a sales opportunity rather than treating them as interchangeable records.

### 4.3 Sales pipeline

- Configurable pipelines.
- Customisable stages.
- Kanban-style opportunity management.
- Deals associated with contacts and conversations.
- Opportunity value.
- Deal ownership.
- Stage-change history.
- Lost and won outcomes.

### 4.4 Website lead capture

Support lead capture from business websites through:

- Embeddable forms or lightweight integration.
- API endpoints.
- Webhook integrations.
- Source and campaign attribution.
- Automatic contact creation or matching.
- Optional WhatsApp follow-up workflows.

The integration should eventually support websites built with different platforms, including WordPress and custom-built websites.

### 4.5 Follow-up and task management

- Follow-up reminders.
- Tasks associated with contacts and deals.
- Due dates.
- Task ownership.
- Overdue follow-up visibility.
- Activity tracking.
- Automated follow-up triggers.

### 4.6 Automation

A visual or otherwise accessible automation system supporting:

- New lead triggers.
- Incoming message triggers.
- Keyword triggers.
- Contact and deal changes.
- Conditional branches.
- Delays and scheduled actions.
- Tag updates.
- Webhooks.
- Follow-up tasks.
- Human handoff.

Automation execution must be reliable. Delayed tasks must not depend solely on fragile, process-local state.

### 4.7 AI assistance

Potential capabilities include:

- Suggested replies.
- Conversation summaries.
- Lead qualification assistance.
- Lead intent classification.
- Follow-up suggestions.
- Knowledge-base-assisted responses.
- Automated responses with appropriate human escalation.

AI functionality should be configurable. Customers should eventually be able to choose their own provider or credentials where practical.

AI must not send sensitive or consequential communications without appropriate customer-configured controls.

### 4.8 Reporting and analytics

The product should eventually report:

- Enquiry volume.
- Lead sources.
- Response times.
- Conversation activity.
- Lead qualification.
- Pipeline value.
- Conversion rates.
- Follow-up performance.
- Team activity.
- Campaign performance where data is available.

Reports must be based on actual recorded events and clearly defined metrics.

### 4.9 Team and permissions

Support:

- Business owners.
- Administrators.
- Agents.
- Read-only users.

Permissions must be enforced on the server and database, not merely hidden in the interface.

### 4.10 Integrations and extensibility

Preserve and evaluate the existing REST API and MCP server.

Future integrations may include:

- Website forms.
- CRM and marketing systems.
- Workflow automation tools such as n8n.
- AI services.
- Additional messaging channels.

Do not introduce unnecessary integrations during the initial implementation.

---

## 5. WhatsApp integration requirements

### 5.1 Preferred integration

Use the official Meta WhatsApp Business Cloud API for production customer accounts.

Avoid relying on unofficial WhatsApp Web automation for customers' business-critical numbers.

### 5.2 Initial testing

Begin with a Meta developer application and test phone number.

Verify:

- Inbound message handling.
- Outbound message sending.
- Webhook verification.
- Webhook signature validation.
- Contact creation and matching.
- Message status updates.
- Template messages.
- Token expiry and renewal considerations.
- Error handling.
- Human handoff.

Use an HTTPS tunnel when exposing the local webhook endpoint during development.

Do not connect a real customer's WhatsApp number until the integration has been tested and the security implications reviewed.

### 5.3 Future onboarding

Investigate the appropriate Meta onboarding process for a multi-customer SaaS product, including business verification, WhatsApp Business Account ownership, phone-number onboarding and embedded signup where applicable.

Do not assume that the initial single-installation integration automatically supports SaaS onboarding.

---

## 6. Architecture and multi-tenancy

### 6.1 Initial architecture

Initially, run one development installation with one isolated Supabase development project.

Understand the existing account-scoped data model before changing it.

Do not attempt a major multi-tenant rewrite during the first development phase.

### 6.2 Intermediate deployment model

Separate installations for individual customers may be used during early commercial validation.

This is an acceptable intermediate approach if it provides reliable customer isolation and manageable operating costs.

### 6.3 Long-term SaaS architecture

The intended long-term architecture is multi-tenant.

It should support:

- Organisations or workspaces.
- Organisation membership.
- Organisation-specific roles and permissions.
- Tenant-owned contacts.
- Tenant-owned conversations.
- Tenant-owned pipelines and deals.
- Tenant-specific WhatsApp integrations.
- Tenant-specific automation rules.
- Tenant configuration.
- Tenant-level usage and billing.
- Central platform administration.

### 6.4 Tenant isolation

Tenant isolation is a critical architectural requirement.

The implementation must eventually provide:

- Explicit organisation ownership for tenant data.
- Strict database-level access controls.
- Appropriate Row Level Security policies.
- Server-side authorisation.
- Protection against cross-tenant API access.
- Secure handling of tenant credentials.
- Audit logs for sensitive actions.
- Tests that attempt to access another organisation's data.

Do not assume that existing account-level Row Level Security automatically provides complete multi-tenant isolation.

### 6.5 Platform administration

A future central administration area should support:

- Organisation management.
- Customer account status.
- Subscription and usage management.
- System health.
- Support and troubleshooting.
- Platform-wide configuration.

This should be designed after the underlying tenant model is understood.

---

## 7. Security and reliability requirements

Security must be treated as a core product requirement rather than a final polishing exercise.

The agent must inspect and document:

1. Authentication and session management.
2. Database Row Level Security.
3. Server-side authorisation.
4. API key handling and revocation.
5. Encryption of sensitive integration credentials.
6. WhatsApp webhook signature validation.
7. Input validation.
8. Rate limiting.
9. Background job and scheduled task reliability.
10. Error handling and logging.
11. Dependency vulnerabilities.
12. Backup and restore procedures.
13. Data deletion and customer offboarding.
14. Tenant isolation before SaaS release.

Never commit:

- `.env.local` files.
- Supabase service-role keys.
- Meta application secrets.
- Access tokens.
- Encryption keys.
- Other production credentials.

Use synthetic test contacts and conversations during development.

Any serious security weakness must be documented and addressed before production use.

---

## 8. Development phases and acceptance criteria

Work must proceed in controlled phases. Each phase requires a report and review before the next implementation prompt is issued.

### Phase 0 — Environment audit

**Objective:** Establish the actual state of the development machine.

Tasks:

- Inspect operating system.
- Inspect memory and available disk space.
- Verify Node.js, npm, nvm and Git.
- Check Git configuration.
- Check Docker availability without installing or modifying it.
- Identify any missing prerequisites.

**Restrictions:** Read-only inspection. No installations or system changes.

**Acceptance criteria:**

- A complete environment audit report.
- Confirmed compatibility with the proposed development workflow.
- List of missing tools, if any.
- Recommended next steps.

### Phase 1 — Repository ownership and project setup

**Objective:** Establish a Tabi-owned working repository.

Tasks:

- Fork wacrm into the user's GitHub account.
- Clone the fork into `~/projects/tabi-lead-system`.
- Configure `origin` as the Tabi fork.
- Configure `upstream` as the original wacrm repository.
- Record the starting commit.
- Establish a baseline tag.
- Review the licence and attribution requirements.
- Create project documentation.
- Establish a sensible branch and commit workflow.

**Acceptance criteria:**

- Working Tabi-owned repository.
- Correct Git remotes.
- Baseline commit and tag.
- Documented licence findings.
- No accidental changes to the upstream repository.

### Phase 2 — Technical and security audit

**Objective:** Understand the actual codebase before modifying it.

Tasks:

- Inspect application structure.
- Inspect dependencies and scripts.
- Inspect environment configuration.
- Inspect database schema and migrations.
- Inspect authentication and RLS policies.
- Inspect WhatsApp integration.
- Inspect API and MCP implementation.
- Inspect automation and background processing.
- Inspect AI integration.
- Identify existing tests and build checks.
- Identify known limitations and risks.

**Acceptance criteria:**

- Architecture report.
- Database and migration report.
- Security findings.
- Dependency and compatibility findings.
- Feature inventory.
- Prioritised technical risk register.
- Recommendations for the first runnable installation.

No major application refactoring during this phase.

### Phase 3 — Untouched local installation

**Objective:** Run the original application locally before customising it.

Tasks:

- Create a separate Supabase development project.
- Configure local environment variables using the repository's actual example and documentation.
- Install dependencies using the appropriate lockfile.
- Run database migrations in the correct order.
- Start the local development server.
- Test registration, login and logout.
- Run the available lint, typecheck and build commands.

**Acceptance criteria:**

- Application accessible locally.
- Authentication works.
- Database connection works.
- Baseline checks completed.
- All failures documented.
- No production database or credentials involved.

### Phase 4 — Functional testing

**Objective:** Determine what works and what needs improvement.

Test:

- Dashboard.
- Inbox.
- Contacts.
- Tags and custom fields.
- Sales pipelines.
- Broadcasts.
- Automations.
- Flows.
- AI features.
- Team accounts.
- Public API.
- MCP server.

Create synthetic leads and test complete workflows.

**Acceptance criteria:**

- Feature-by-feature test report.
- Working functionality identified.
- Broken or incomplete functionality identified.
- Usability observations.
- Prioritised gap list.

### Phase 5 — WhatsApp integration validation

**Objective:** Confirm that the official Meta integration works reliably.

Tasks:

- Set up a Meta developer application.
- Configure a test WhatsApp number.
- Configure credentials.
- Expose the local webhook through HTTPS.
- Test inbound and outbound messages.
- Test message status updates.
- Test templates.
- Test webhook validation and invalid signatures.
- Document token and credential management.

**Acceptance criteria:**

- Successful inbound and outbound test.
- Verified webhook behaviour.
- Documented error handling.
- Security review of integration.
- Test evidence.

### Phase 6 — Tabi product customisation

**Objective:** Begin transforming the base CRM into Tabi Lead System.

Implement features incrementally, using separate branches and reviewable batches.

Suggested order:

1. Product identity and branding.
2. Improved lead profiles and custom fields.
3. Website lead capture.
4. Lead-source attribution.
5. Follow-up tasks and reminders.
6. Improved pipeline workflows.
7. Customer-specific configuration.
8. Reporting and analytics.
9. AI-assisted lead qualification.
10. Additional integrations.

The actual order may be adjusted after the audits.

**Acceptance criteria for each batch:**

- Clear scope.
- Implementation report.
- Tests and verification evidence.
- No unexplained regressions.
- Updated documentation.
- Review approval before the next batch.

### Phase 7 — Multi-tenant architecture

**Objective:** Prepare the product for multiple customer organisations.

Tasks:

- Design the organisation and membership model.
- Map existing user ownership and data relationships.
- Design tenant-aware database policies.
- Implement tenant-aware application services.
- Add organisation-level permissions.
- Secure tenant-specific integrations.
- Test cross-tenant isolation.
- Introduce central administration foundations.

**Acceptance criteria:**

- Approved architecture design.
- Documented migration strategy.
- Verified tenant isolation.
- Automated security tests.
- No cross-tenant data access.
- Documented rollback strategy.

This phase requires a dedicated architecture review before implementation.

### Phase 8 — Product hardening and production readiness

**Objective:** Prepare a dependable commercial product.

Tasks:

- Production deployment.
- Monitoring and alerting.
- Backup and restore.
- Rate limiting and abuse protection.
- Performance testing.
- Security review.
- Error tracking.
- Customer onboarding.
- Data export and deletion.
- Documentation.
- Operational procedures.

### Phase 9 — Commercial SaaS capabilities

**Objective:** Introduce the business infrastructure required to sell the platform as a service.

Potential capabilities:

- Subscription plans.
- Billing integration.
- Usage limits.
- Organisation provisioning.
- Trial accounts.
- Account suspension and reactivation.
- Customer administration.
- Support workflows.
- Product usage analytics.

Do not implement billing until the product's core architecture and customer model are stable.

---

## 9. Agent implementation protocol

### 9.1 Division of responsibilities

**Command Code agent**

Responsible for:

- Repository inspection.
- Technical audits.
- Implementation.
- Tests.
- Documentation.
- Git operations within approved scope.
- Producing detailed reports.

**ChatGPT reviewer and project coordinator**

Responsible for:

- Reviewing agent reports.
- Assessing implementation quality and completeness.
- Identifying omissions, risks and incorrect assumptions.
- Requesting corrections.
- Issuing the next scoped implementation prompt.
- Maintaining alignment with this specification.

**Project owner**

Responsible for:

- Approving major architectural and product decisions.
- Providing credentials and external account access when needed.
- Reviewing business priorities.
- Approving production deployments and consequential changes.

### 9.2 Batch-based execution

The agent must not attempt to implement the entire project in one task.

Every task must have:

1. A defined objective.
2. Explicit scope.
3. Files or areas likely to be affected.
4. Restrictions.
5. Verification requirements.
6. Documentation requirements.
7. A completion report.

The agent must stop after completing the assigned task and wait for review.

### 9.3 Reporting

Reports should be saved under:

`docs/reports/`

Each report should include:

- Date.
- Phase and task identifier.
- Objective.
- Work completed.
- Files changed.
- Commands executed.
- Tests performed.
- Test results.
- Outstanding issues.
- Risks discovered.
- Decisions required.
- Recommended next step.
- Git branch and commit information, where applicable.

The agent must distinguish between:

- Implemented and verified.
- Implemented but not verified.
- Partially implemented.
- Not implemented.
- Blocked.

It must never claim successful completion without evidence.

### 9.4 Change management

- Use Git branches for meaningful implementation batches.
- Keep commits focused and descriptive.
- Do not rewrite upstream history.
- Do not force-push.
- Do not delete project data or migrations without approval.
- Do not change the technology stack without justification.
- Do not deploy to production without explicit approval.
- Do not modify unrelated projects or system configuration.

### 9.5 Agent instructions

The project should have a root-level `AGENTS.md` containing persistent instructions for Command Code.

It should include:

- Product vision.
- Architecture principles.
- Development workflow.
- Security requirements.
- Testing standards.
- Reporting requirements.
- Prohibited actions.
- Rules for working with upstream changes.

The agent must read and follow this file before performing implementation work.

---

## 10. Documentation structure

Maintain a clear project documentation system.

Proposed structure:

```text
tabi-lead-system/
├── AGENTS.md
├── README.md
├── docs/
│   ├── project-specification.md
│   ├── roadmap.md
│   ├── architecture/
│   │   ├── system-overview.md
│   │   ├── database-design.md
│   │   └── decisions/
│   ├── audits/
│   ├── reports/
│   ├── testing/
│   ├── deployment/
│   └── security/
├── src/
├── supabase/
└── ...
```

This is a proposed documentation layout, not an instruction to restructure the application source directories. Preserve the upstream project's existing structure unless there is a justified reason to change it.

---

## 11. Definition of success

The initial project will be considered technically successful when:

- The application runs reliably in a local development environment.
- The official WhatsApp Cloud API works with a test account.
- Teams can manage contacts and conversations.
- Leads can be tracked through sales pipelines.
- Website enquiries can enter the CRM.
- Follow-up tasks and basic automations work.
- Security and access controls have been tested.
- The custom product direction is documented.
- The project can be maintained independently of the original repository.

The longer-term commercial objective is a secure multi-tenant platform that Tabi Digital can deploy, operate and sell to multiple businesses.

---

## 12. Guiding principles

1. **Understand before changing.** Audit the existing code before modifying it.
2. **Build incrementally.** Prefer small, testable implementation batches.
3. **Preserve useful upstream functionality.** Avoid unnecessary rewrites.
4. **Security before convenience.** Especially for customer data and WhatsApp credentials.
5. **Official integrations for production.** Prioritise the official Meta Cloud API.
6. **Self-hostability matters.** Avoid unnecessary vendor lock-in.
7. **Keep operating costs manageable.** Avoid premature infrastructure complexity.
8. **Design for multi-tenancy, implement it deliberately.**
9. **Document decisions and evidence.** Reports are part of the deliverable.
10. **Human review at every milestone.** The agent implements; the reviewer validates and authorises the next stage.

---

## 13. Immediate next action

Begin with **Phase 0 — Environment Audit**.

The agent should:

- Read this specification.
- Inspect the development environment using read-only commands.
- Avoid installing, updating or removing anything.
- Avoid modifying system configuration.
- Save the results in `docs/reports/`.
- Provide a concise summary of compatibility, missing prerequisites and recommended next steps.

Stop after submitting the report.

No repository cloning, application installation, database creation or code modification is authorised during Phase 0.

**End of specification.**
