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

---

## Steps

### 1 — Read the PR

Read the PR title, description, and diff. Identify:
- Which task this implements (look up in BACKLOG.md)
- Which domain(s) the change touches
- Whether any security-sensitive areas are involved

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

### 5 — Post Review

Post the synthesised review to the PR. Do not post individual reviewer outputs — post the synthesis.

If changes are requested, the implementer addresses them and the workflow is re-run on the updated PR.
