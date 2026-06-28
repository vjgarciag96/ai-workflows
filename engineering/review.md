# Workflow: Review

## Purpose

Review a PR with domain-primary reviewers and cross-domain crosspollination. Synthesise findings and either approve or request changes.

## Input

- A PR (branch name or PR reference)
- `spec/engineering/TECH_SPEC.md`
- `spec/design/DESIGN.md`
- The codebase

## Output

- Synthesised review findings
- Explicit approval or a prioritised list of requested changes
- PR updated with review comments

---

## Principles

- Domain-primary reviewers catch implementation errors. Cross-domain reviewers catch integration errors. Both are necessary.
- Neville is always in the review pool. QA perspective on every PR catches issues before they compound.
- Moody joins any PR that touches authentication, tokens, permissions, or user data.
- Reviewers do not see each other's output before writing their own.
- The synthesis distinguishes blockers (must fix before merge) from suggestions (worth doing, not required) from observations (noted, no action needed).
- Approve means the PR is ready to merge as-is. Request changes means it is not. There is no middle ground.
- CI must pass before merging, not before approval. Approval and CI are independent gates — both must be satisfied before a PR is merged.
- AI agent comments (GitHub Copilot, etc.) are part of the review input. Read them, validate them, and address them in the synthesis — do not silently ignore them.
- Review findings are posted to the GitHub PR as a formal review with inline comments where possible, not just noted internally.

---

## Steps

### 1 — Read the PR

Read the PR title, description, and diff. Identify:
- Which task this implements (look up in BACKLOG.md)
- Which domain(s) the change touches
- Whether any security-sensitive areas are involved

Fetch all existing PR comments, including those from GitHub Copilot or other AI agents. Treat them as additional input — they may surface issues the review team should validate, confirm, or rebut. Do not ignore them because they came from a tool.

---

### 2 — Assemble the Review Team

Select reviewers based on the domain(s) touched:

**Domain-primary (always include):**
- `android` → Harry
- `backend` → Hermione
- `web` → Ron
- `infra` → Arthur

**Always include:**
- Neville — QA perspective on every PR
- Dumbledore — if the change touches architectural boundaries

**Always include when relevant:**
- Moody — any PR touching auth, tokens, permissions, or user data
- McGonagall — any PR touching UI or screen states
- Ginny — any PR touching API contracts or client-server protocol

**Cross-domain crosspollination (pick one):**
- Add one reviewer from outside the primary domain. Rotate — do not always pick the same person. Cross-domain reviewers often catch the integration issues that domain experts miss.

---

### 3 — Run Reviews in Parallel

Launch one agent per reviewer simultaneously. Each receives:
- The PR diff
- The task's ACs from BACKLOG.md
- The relevant sections of TECH_SPEC.md
- Their character from `team/`

Each reviewer produces:
- **Blockers** — issues that must be fixed before merge (correctness, security, AC violations)
- **Suggestions** — improvements worth making but not blocking
- **Observations** — things noticed that need no action

200–300 words per reviewer, in character.

---

### 4 — Synthesise

Group findings across all reviewers:

1. **Blockers** — consolidate duplicates, rank by severity. These must all be resolved before the PR merges.
2. **Suggestions** — worth surfacing to the implementer, not required.
3. **Observations** — log for awareness.

If there are no blockers: approve.
If there are blockers: request changes, listing them clearly.

---

### 5 — Check CI

Check the CI status on the PR and include it in the posted review. CI and approval are independent gates — both must pass before merging. A PR can be approved while CI is still running, but it must not be merged until all required checks pass.

---

### 6 — Post Review to GitHub

Post the synthesised review as a GitHub PR review using `gh pr review`. Use inline comments for specific line-level findings where possible — not just a top-level comment. Post the overall summary and decision (approve / request changes) as the review body.

Do not post individual reviewer outputs — post the synthesis only.

If changes are requested, the implementer addresses them and the workflow is re-run on the updated PR.
