# Workflow: Plan

## Purpose

Slice a signed-off tech spec into a prioritised, assigned backlog ready for implementation. The output is a vertical slices narrative and a hierarchical markdown backlog.

## Input

- `spec/engineering/TECH_SPEC.md`
- `spec/product/PRD.md`
- `spec/design/DESIGN.md`

## Output

- `spec/engineering/SLICES.md` — vertical slices narrative: what each slice delivers end-to-end, why this order
- `spec/engineering/BACKLOG.md` — full hierarchy: Epic → Story → Task, each with owner, domain, ACs, dependencies, and status

---

## Principles

- Slice vertically, not horizontally. Each slice delivers something end-to-end — a user can do something after it ships. Slicing by layer (all backend first, then all frontend) is not a slice.
- Dependencies flow forward. Later slices depend on earlier ones, never the reverse.
- Tasks must be small enough for one person to implement and review in a single session. If a task takes more than a day, split it.
- Every task has one owner. Shared ownership is no ownership.
- Acceptance criteria are written at the story level (what the user experiences) and the task level (what the implementation must do). Both matter.
- The backlog is a living document. Tasks added during QA or validation are appended, not inserted.

---

## Steps

### 1 — Read the Inputs

Read TECH_SPEC.md, PRD.md, and DESIGN.md in full before launching any reviewers.

---

### 2 — Run the Slicing Team in Parallel

Launch one agent per team member simultaneously. Each receives all three documents and their character from `team/`. Goal: surface slice boundaries, task breakdowns, and sequencing constraints before any structure is committed to.

**Do not let reviewers see each other's output at this stage.**

- **Dumbledore** — architectural slice boundaries; what must exist before what; decisions that force ordering; shared foundations that multiple slices depend on
- **Percy** — scope discipline; story sizing (too big = split, too vague = specify); AC completeness; what "done" means for each story
- **Harry** — Android task granularity; platform-specific sequencing (permissions before features that need them, etc.); what a junior will struggle to implement without more context
- **Hermione** — backend task boundaries; API dependency ordering; what the client cannot build until the server has shipped
- **Arthur** — infrastructure prerequisites; what must be deployed before any other task can be tested; operational tasks that are easy to forget until they block everything
- **Neville** — testability of each proposed task; which tasks need test infrastructure before they can be validated; AC gaps that will make QA impossible

Each reviewer: 200–300 words. A concrete list of slice boundaries and sequencing constraints — not a general review.

---

### 3 — Synthesise and Propose Slices

Combine the slicing team's input into a proposed vertical slice structure. For each slice:

- What it delivers end-to-end (one sentence)
- Why it comes in this position
- Which epics it contains
- What it depends on and what it unblocks

Present to the product owner. Resolve any sequencing disagreements before proceeding.

---

### 4 — Write SLICES.md

Save to `spec/engineering/SLICES.md` using this structure:

```
# Vertical Slices — [Project Name]

## Slice N: [Name]
**Delivers:** one sentence — what a user can do after this slice ships
**Why here:** why this position in the sequence
**Epics:** list of epic names
**Depends on:** previous slices or none
**Unblocks:** subsequent slices
```

---

### 5 — Write BACKLOG.md

Save to `spec/engineering/BACKLOG.md` using this structure:

```
# Backlog — [Project Name]

## Epic N: [Name]
**Slice:** N

### Story N.N: [Name]
**ACs:**
- [ ] user-facing acceptance criterion

#### Task N.N.N: [Name]
**Owner:** [team character name]
**Domain:** [android | backend | web | infra | design | qa]
**Status:** todo
**Dependencies:** [Task N.N.N | none]
**ACs:**
- [ ] implementation-level acceptance criterion
```

**Status values:** `todo` | `in-progress` | `in-review` | `done` | `blocked`

**Owner values:** team character names from `team/`. One owner per task.

Every task must have at least one AC. Every story must have at least one AC. No AC may be vague enough to pass without a clear check.

---

### 6 — Commit

Commit SLICES.md and BACKLOG.md together. Message describes what the planning phase produced.
