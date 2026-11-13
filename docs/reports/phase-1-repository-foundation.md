# Phase 1 — Repository Foundation Report

| Field | Value |
|---|---|
| **Date** | 2026-11-13 |
| **Phase / task** | Phase 1 — Repository ownership and project setup |
| **Branch** | `main` |
| **Status** | Complete. Awaiting human review. Phase 2 has not been started. |

**Status labels used:** **Verified** means observed directly by a command whose output I read. **Not verified** means I could not or did not confirm it. **Partially verified** means only part of it was confirmed. **Blocked** means it could not be done.

---

## 1. Executive summary

- **Verified.** I forked `ArnasDon/wacrm` to `ahmedk-dev/tabi-lead-system` after confirming the upstream licence is MIT. The fork is public and keeps its fork relationship.
- **Verified.** The existing local directory is now a Git repository on `main`. It holds the unmodified upstream tree at commit `c81299d` plus all Tabi project resources.
- **Verified.** I created the baseline commit `069e408` and the annotated tag `tabi-baseline-0.1.0`. A second commit, `b93154e`, adds the documentation. Both commits and the tag are on the Tabi fork. Nothing was pushed to `upstream`.
- **Verified.** I did not install dependencies, run the application, or modify any application source.
- **Not verified.** Whether GitHub Actions CI runs on the fork. Zero runs existed when I checked (section 11).

---

## 2. Upstream repository and licence findings

All values below are **Verified** via the GitHub API and file reads.

| Item | Finding |
|---|---|
| Repository | `ArnasDon/wacrm`, public, not archived, forking allowed |
| Default branch | `main` |
| Latest commit | `c81299d1488aac02fa584f68d97c2524c1e7a661`, "Merge pull request #721 from ArnasDon/fix/707-native-context-menu", dated 2026-10-30 |
| Size and tree | 647 tracked files. Tags: none. The upstream tree listing was not truncated. |
| Licence | **MIT**, "Copyright (c) 2026 Arnas Donauskas". I read the full text of `LICENSE`. |
| Licence obstacle | **None found.** MIT permits use, modification, distribution and commercial use, provided the copyright and permission notice stay in all copies. |
| Fork conditions (`CONTRIBUTING.md`, "If you maintain a public fork") | (1) The upstream name "CRM Template for WhatsApp", its favicon and the `wacrm.tech` URL "belong to the upstream project". Swap them for your own before putting a deployment in front of users. (2) Keep the `LICENSE` file. (3) README attribution is appreciated but not required. (4) Additions to the fork may be licensed freely. |
| `package.json` | `name: wacrm`, `version: 0.8.0`, `license: MIT`, `engines.node: >=22.12.0` |
| Top-level structure | `src/`, `supabase/`, `mcp-server/`, `messages/`, `public/`, `docs/`, `.github/`, `Dockerfile`, `docker-compose.yml`, `package.json`, `package-lock.json`, `AGENTS.md`, `CLAUDE.md`, `README.md`, `CHANGELOG.md`, `CONTRIBUTING.md` and config files |
| Agent files | `AGENTS.md` (5 lines, a Next.js warning block only) and `CLAUDE.md` (the single line `@AGENTS.md`) |
| Upstream `docs/` | `auth-emails.md`, `docker.md`, `mcp.md`, `multi-waba.md`, `public-api.md`, `whatsapp-connection-troubleshooting.md` |
| Migrations | 57 files in `supabase/migrations/`, named `001`–`059`. `050_` and `056_` are absent, so there are numbering gaps. |
| Tests | 158 `*.test.ts(x)` files tracked. **Not run.** |
| Env files tracked | Only `.env.local.example` and `mcp-server/.env.example`. No real `.env` files. |
| Conflicts with local content | **None at file level.** Upstream and local both have a `docs/` directory, but they share no filenames. |

---

## 3. GitHub fork details

| Item | Value | Status |
|---|---|---|
| URL | https://github.com/ahmedk-dev/tabi-lead-system | Verified |
| Created | 2026-11-13T14:43:31Z | Verified |
| Fork relationship | `fork=true`, `parent=ArnasDon/wacrm`, `source=ArnasDon/wacrm` | Verified |
| Visibility | **Public.** Inherited from upstream. I did not change it. | Verified |
| Default branch | `main` | Verified |
| Name conflict | None. The name `tabi-lead-system` was free before the fork (a 404 on the repo lookup). | Verified |
| Command used | `gh repo fork ArnasDon/wacrm --fork-name tabi-lead-system --clone=false` | Verified |

---

## 4. Local integration approach

1. **Cloned into a temporary sibling.** I cloned the Tabi fork (not upstream directly) to `~/projects/.tabi-lead-system-tmp-clone`. Its `main` was at `c81299d`, identical to upstream, which I confirmed with `git ls-remote upstream`. This is a small deviation from "obtain the upstream repository" (section 11).
2. **Checked for conflicts.** I compared the root names and the `docs/` filenames. Upstream and local shared no file.
3. **Recorded the spec hash.** The SHA-256 of the spec before integration was `366c8689…a081`.
4. **Copied the upstream files in.** I used `tar … --keep-old-files`, which refuses to overwrite existing files. The copy excluded `.git`.
5. **Initialised Git.** I ran `git init -b main` in the project directory and set local-only `user.name` and `user.email`. I added `origin` and `upstream`, ran `git fetch`, then ran a mixed `git reset origin/main`. That set the index to upstream's tree without touching the working tree.
6. **Checked the result.** `git status` showed only the Tabi paths as untracked: `.commandcode/`, `docs/reports/` and `docs/resources/`. No upstream-tracked file was modified or deleted.
7. **Removed the temporary clone.** I confirmed afterwards that `~/projects/.tabi*` does not exist and the `~/projects` listing contains no stray directories.

**Why the history is preserved.** The baseline commit is a child of upstream's `c81299d`. It is not an orphan initial commit. This keeps `git log main..upstream/main` meaningful for later upstream reviews.

---

## 5. Git configuration and remotes

| Item | Value | Status |
|---|---|---|
| `user.name` (local) | `Ahmed` | Verified |
| `user.email` (local) | `amed.kivumbi@gmail.com` | Verified |
| Global Git config | Unchanged. It already held the same name and email. I made no `--global` calls. | Verified |
| Commit authors | Both commits show `Ahmed <amed.kivumbi@gmail.com>` | Verified |
| `origin` fetch and push | `https://github.com/ahmedk-dev/tabi-lead-system.git` | Verified |
| `upstream` fetch and push | `https://github.com/ArnasDon/wacrm` | Verified |
| Push destination checked first | I printed `git remote get-url --push origin` and queried the fork's parent via the API before pushing | Verified |
| Pushed to upstream | **No.** `git ls-remote upstream` still shows `c81299d`. | Verified |
| Machine-local settings | `.commandcode/settings.json` is excluded through `.git/info/exclude`. I confirmed it with `git check-ignore -v`. | Verified |

**Note on `upstream` push URL.** The `upstream` remote has a push URL, because I did not set `pushurl` to a disabled value. Nothing was pushed to it. If you want a hard guard, a disabled push URL could be added (a recommendation, not done).

---

## 6. Commits, branch and tag

| Item | Value | Status |
|---|---|---|
| Branch | `main` | Verified |
| Upstream base | `c81299d1488aac02fa584f68d97c2524c1e7a661` | Verified |
| Baseline commit | `069e408eefa12813689c2b73336307ad6dae76a4`, "chore: establish Tabi Lead System project baseline" | Verified |
| Documentation commit | `b93154e6759950deed0b7479900870878ad2a7b0`, "docs: add Tabi agent rules, README section and area READMEs" | Verified |
| Tag | `tabi-baseline-0.1.0`, **annotated**, tag object `aa4bf73…`, pointing at `069e408` | Verified |
| On the fork | `refs/heads/main` is `b93154e` and the tag peels to `069e408`. I confirmed both with `git ls-remote origin`. | Verified |
| This report's commit | Not recorded here, because a file cannot contain its own commit hash. See `git log` for the commit that adds it. | Not applicable |

**The tag marks the baseline before the Tabi documentation was added.** It points at `069e408`, not at the docs commit. It contains the unmodified upstream tree plus the spec, the Phase 0 report, `.commandcode/` and the taste file. `AGENTS.md` and the new README section arrive one commit later. This is intentional, so the tag stays a clean "upstream plus resources" reference. I recorded it here so the difference is visible.

---

## 7. Documentation created

| File | Action | Notes |
|---|---|---|
| `AGENTS.md` | Updated | The upstream 5-line block is kept **byte-identical** at the top (confirmed with `diff`). The Tabi block is appended between `tabi-agent-rules` markers. |
| `README.md` | Updated | A Tabi block is prepended between `tabi-readme` markers. The entire upstream README follows it **unchanged** (confirmed with `diff`). |
| `docs/architecture/README.md` | Created | Placeholder |
| `docs/audits/README.md` | Created | Placeholder |
| `docs/testing/README.md` | Created | Placeholder. It lists the upstream npm scripts and states that none has been run. |
| `docs/security/README.md` | Created | Placeholder. It records the binding requirements from spec sections 6.4 and 7. |
| `docs/deployment/README.md` | Created | Placeholder |
| `docs/reports/phase-1-repository-foundation.md` | Created | This report |

`AGENTS.md` covers all ten topics the prompt listed: vision and scope, document hierarchy, phased development with the stop rule, inspect-before-modify, security and tenant isolation, testing expectations, reporting, prohibited actions, upstream handling, and licence.

**Not done.** `CLAUDE.md` is unchanged. It imports `AGENTS.md`, so it picks up the Tabi block automatically.

**Accuracy approach.** The documents describe the repo as unmodified upstream and state that nothing has been installed, configured or run. The area READMEs are labelled placeholders. No planned feature is described as existing. I did not create `docs/project-specification.md`, `docs/roadmap.md` or any subdirectory the prompt did not list.

---

## 8. Files preserved

All **Verified.**

- **The specification** is byte-identical to its pre-integration state. Its SHA-256 `366c86899aa2b81c88a99b2aba01fa2f9a538d9539432e4e28a8fa644c85a081` matched before and after, and `git diff` shows no change since the baseline commit.
- **`.commandcode/`** is identical to its state in the baseline commit. That covers the three project skills (`supabase`: 4 tracked files, `supabase-postgres-best-practices`: 36, `vercel-react-best-practices`: 76, each with `SKILL.md`) and `taste/taste.md` (0 bytes, untouched).
- **`docs/reports/phase-0-environment-audit.md`** is preserved and committed.
- **`LICENSE`** is tracked and unmodified.
- **Upstream source.** Outside the Tabi paths, the baseline commit's tree equals upstream `c81299d`. Of the 522 tracked files under `src/`, none has changed. `git diff` against upstream shows no change in `src/`, `supabase/`, `package.json`, `package-lock.json`, `mcp-server/` or `next.config.ts`.

---

## 9. Security and secret checks

| Check | Result | Status |
|---|---|---|
| `.env*`, `*.pem`, `*.key` files in the working tree | Only the two upstream `*.example` templates | Verified |
| `.env*` files staged or committed | None | Verified |
| Regex scan of untracked files and of both staged diffs (GitHub tokens `gho_`/`ghp_`/`github_pat_`, `sk-…`, AWS `AKIA…`, JWT shapes, private-key headers, populated `SUPABASE_SERVICE_ROLE_KEY=` or `ENCRYPTION_KEY=` values) | No matches in anything committed | Verified |
| `.commandcode/settings.json` | Contains only shell-command permission strings with local paths, no credentials. **Excluded from Git** and never committed. | Verified |
| `.gitignore` (upstream) | Ignores `.env*` except the two examples, plus `*.pem`, `node_modules`, `.next`. I did not modify it. | Verified |
| `gh` token | Never printed or recorded. It is stored in the system keyring. | Verified |
| Scan limits | The regex scan is a heuristic. It is not a full secret-scanning tool such as gitleaks, which is not installed. It does not cover the upstream history that arrived with the fork. | Partially verified |

---

## 10. Verification results

| Requirement | Result | Status |
|---|---|---|
| Git repository initialised | `git init -b main` succeeded | Verified |
| Correct branch and commit | `main` at `b93154e` | Verified |
| Local author identity | `Ahmed <amed.kivumbi@gmail.com>` | Verified |
| `origin` and `upstream` URLs | As in section 5 | Verified |
| Baseline commit and tag exist locally | Yes | Verified |
| Branch and tag on the fork | Yes (`git ls-remote origin`) | Verified |
| Spec intact | Hash match | Verified |
| `.commandcode/` and all 3 skills intact | Yes | Verified |
| Upstream source present | 647 upstream files plus the Tabi additions | Verified |
| No secrets committed | See section 9 | Partially verified |
| No application code modified | `git diff` against upstream is empty for source paths | Verified |
| New docs accurate and consistent | I checked that every linked file exists and that the upstream blocks are unchanged. I did not run a link checker. | Partially verified |
| Dependencies not installed | `node_modules/` does not exist | Verified |
| No Supabase, database, WhatsApp or deployment actions | None were taken | Verified |
| `npm run lint`, `typecheck`, `test`, `build` | **Not run.** Out of scope for Phase 1. | Not verified |

---

## 11. Problems, deviations and unresolved decisions

### Deviations

1. **Cloned the fork rather than upstream into the temporary directory.** The fork's `main` was identical to upstream at `c81299d`, confirmed by `git ls-remote upstream`.
2. **Added the documentation as a second commit,** rather than putting it in the baseline commit. The prompt asked for documentation to be created, and it needed the baseline's file list to be accurate first.
3. **Pushed the documentation commit** to the fork's `main` in addition to the baseline. The prompt authorised pushing the baseline branch to the fork, and I treated the docs commit as part of that branch.
4. **A shell error mid-run.** One verification command used bash process substitution under `sh` and failed with a syntax error. I re-ran it under `bash` and it passed. Nothing was changed by the failed run.

### Findings and open issues

1. **CI on the fork is unconfirmed.** `gh run list` returned nothing and the Actions API reported `total_count: 0`, although Actions is `enabled` at repo level and `ci.yml` triggers on pushes to `main`. This may be a delay, or GitHub may require workflows to be enabled on a new fork. **Not verified.** Check the Actions tab before relying on CI.
2. **The fork inherited 314 branches** from upstream (`gh api …/branches` count). I did not delete any, because branch deletion is prohibited without approval. This is clutter, not a risk.
3. **Upstream owner references remain.** `.github/CODEOWNERS` names `@ArnasDon` on every path, and `.github/dependabot.yml` lists `ArnasDon` as a reviewer in two places. I did not change them (upstream files, minimal edits). If Dependabot runs on the fork it may request reviews from the upstream owner. I did not verify whether Dependabot is active on the fork.
4. **Upstream's Hostinger referral links** (`REFERRALCODE=WACRMHOST`) are still in the upstream README section, in five places. They are affiliate links for the upstream author. They fit the later rebranding task.
5. **`.github/SECURITY.md` is upstream's policy.** It tells reporters to contact upstream. A decision is needed on who receives security reports for the fork.
6. **Upstream inconsistencies noticed.** `package.json` says version `0.8.0` while `CHANGELOG.md`'s latest entry is `0.8.1`. `.env.local.example` refers to `docs/automations-and-cron.md`, which does not exist. Both are upstream's. I recorded them and changed nothing.
7. **Public repository and email.** The fork is public, so the commit email `amed.kivumbi@gmail.com` is visible in the public history. This is the identity you specified. It resolves the Phase 0 question only if you accept it as intended. GitHub's noreply address would avoid exposing it.
8. **Phase 0 items not addressed in Phase 1.**
   - `NODE_ENV=production` in the agent shell. It matters at Phase 3 install time.
   - npm 12.2.0 versus the spec's 11.17.0. Upstream's `engines` requires only Node `>=22.12.0`, and upstream pins npm 10 for Dependabot per a branch name (`chore/pin-npm-10-for-dependabot`), which I saw but did not read.
   - The empty `taste.md`.
9. **Spec path.** The spec lives at `docs/resources/tabi-lead-system-spec-doc.md`, not at the `docs/project-specification.md` that spec section 10 proposes. I left it where it is, as instructed.

### Decisions required from the owner

1. Keep the fork **public** or change it. I retained the inherited visibility. Changing it is your call.
2. Accept the public Git email, or switch to a noreply address for future commits.
3. Who should receive security reports for the fork (`.github/SECURITY.md`).
4. Whether to add a disabled push URL on `upstream` as a guard.
5. Whether to prune the 314 inherited branches.

---

## 12. Recommended next phase

**Phase 2 — Technical and security audit** (spec section 8), once you approve.

Suggested scope for the Phase 2 prompt (recommendations, not done):
- Read the code and migrations, **without installing anything**.
- Record the numbering gaps (`050`, `056`) and how migrations are replayed.
- Inspect RLS and account-scoped authorisation, since the spec warns against assuming it isolates tenants.
- Inspect webhook signature validation, encryption of credentials, API-key handling and automation reliability.
- Produce the risk register the spec requires.

Before Phase 3, settle the `NODE_ENV` and npm questions from Phase 0.

---

## 13. Commands executed (summary)

- **Upstream inspection (read-only):** `gh api` calls for repository metadata, the latest commit, branches, tags, the file tree and file contents (`LICENSE`, `AGENTS.md`, `CLAUDE.md`, `.gitignore`, `.env.local.example`, `README.md`, `package.json`, `CONTRIBUTING.md`).
- **Fork:** `gh repo fork ArnasDon/wacrm --fork-name tabi-lead-system --clone=false`.
- **Integration:** `git clone` of the fork into a temporary directory, comparison scripts, `tar … --keep-old-files`, then removal of the temporary directory.
- **Git setup:** `git init -b main`, local `git config`, `git remote add` ×2, `git fetch` ×2, `git reset -q origin/main`, an append to `.git/info/exclude`.
- **Commits:** `git add -A`, `git commit` ×2, `git tag -a tabi-baseline-0.1.0`.
- **Push:** `git push origin main tag tabi-baseline-0.1.0`, then `git push origin main`. Both targeted the fork only.
- **Verification:** `git ls-remote`, `git diff`, `git log`, `sha256sum`, `diff`, `grep` secret scans, `gh run list`, `gh api` for repo and Actions state.

## 14. Files changed

- **Created by Phase 1:** `docs/architecture/README.md`, `docs/audits/README.md`, `docs/testing/README.md`, `docs/security/README.md`, `docs/deployment/README.md`, `docs/reports/phase-1-repository-foundation.md`.
- **Modified:** `AGENTS.md` (Tabi block appended), `README.md` (Tabi block prepended).
- **Brought in unchanged:** the upstream tree (647 files).
- **Locally modified, not committed:** `.commandcode/settings.json` (machine-local, excluded from Git).
