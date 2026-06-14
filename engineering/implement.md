# Workflow: Implement

## Purpose

Implement a single task from the backlog, in character as the assigned team member, following TDD. Open a PR when done.

## Input

- A task ID or name from `spec/engineering/BACKLOG.md`
- `spec/engineering/TECH_SPEC.md`
- `spec/design/DESIGN.md`
- The codebase

## Output

- Implemented code with tests
- A PR opened against the main branch
- Task status updated to `in-review` in BACKLOG.md

---

## Principles

- Implement in character. The assigned team member's experience level and domain shape how the task is approached. Harry asks questions a junior would ask. Hermione is meticulous about edge cases. Implement as they would.
- Test first. Write a failing test before writing any implementation. The test is the spec.
- One task at a time. Do not implement adjacent tasks opportunistically. If a gap is discovered, add it to the backlog and continue.
- The tech spec is authoritative. When in doubt about a choice, the spec decides. If the spec is silent, flag it rather than inventing a solution.
- Small, focused commits. Each commit should represent one coherent change. Do not bundle unrelated changes.
- Do not gold-plate. Implement what the task requires. Leave the next task for the next task.

---

## Steps

### 1 — Read the Task

Read the task from BACKLOG.md. Confirm:
- Status is `todo`
- All dependencies are `done`
- ACs are clear enough to test against

If dependencies are not met or ACs are ambiguous, do not proceed — flag the blocker and stop.

Update the task status to `in-progress` in BACKLOG.md.

---

### 2 — Adopt the Team Member Persona

Read the assigned owner's character file from `team/`. Implement as that person — their seniority, their domain expertise, their instincts. A junior engineer asks more questions and adds more comments. A senior engineer makes deliberate choices and leaves less to chance.

---

### 3 — Understand the Context

Read the relevant sections of TECH_SPEC.md and DESIGN.md for this task. Do not read the full documents unless necessary — read what the task requires.

Understand:
- What the task must produce
- What it must not break
- What interfaces it must conform to

---

### 4 — Write the Tests First

Write failing tests that encode the task's ACs. Each AC should have at least one test. Tests should:
- Be specific to the AC, not to the implementation
- Cover the happy path and at least one failure case
- Use the testing patterns already established in the codebase

Do not write implementation code until the tests exist and fail for the right reason.

---

### 5 — Implement

Write the implementation to make the tests pass. Keep it minimal — only what the tests require. Refactor for clarity once tests are green.

Follow existing code conventions. Do not introduce new patterns without a reason the tech spec supports.

---

### 6 — Self-Review

Before opening the PR, review the change:
- All tests pass
- ACs are covered by tests
- No unintended side effects on adjacent code
- Commit messages are clear
- No debugging artefacts or commented-out code

---

### 7 — Open PR and Update Backlog

Open a PR with:
- Title: `[Task N.N.N] [task name]`
- Body: the task ACs as a checklist, plus any implementation notes worth surfacing for reviewers

Update the task status to `in-review` in BACKLOG.md. Commit the backlog update separately from the implementation.
