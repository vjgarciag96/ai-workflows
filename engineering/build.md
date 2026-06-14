# Workflow: Build

## Purpose

Orchestrate a build cycle: pick up all available tasks from the backlog, implement them in parallel, send each to review, and repeat until the milestone is complete or blocked.

## Input

- `spec/engineering/BACKLOG.md`
- A milestone or slice to build (or "next available" to pick up whatever is unblocked)

## Output

- Implemented and reviewed tasks with status updated to `done`
- A build summary: what was completed, what is blocked, what remains

---

## Principles

- Tasks run in parallel when their dependencies allow it. Do not serialise work that can happen simultaneously.
- Each task is implemented and reviewed before the next cycle picks up dependent tasks. Merging unreviewed code unblocks nothing — it just moves the problem forward.
- Blockers surface immediately. If a task cannot proceed, the cycle notes it and continues with other available tasks rather than stalling.
- The build cycle does not make product decisions. If a task surfaces a decision that isn't in the spec, it stops and flags it rather than deciding.
- The cycle ends when the milestone is complete, all remaining tasks are blocked, or the product owner stops it.

---

## Steps

### 1 — Read the Backlog

Read BACKLOG.md. For the target milestone or slice, identify all tasks grouped by status:

- `todo` with all dependencies `done` → **available**
- `todo` with unmet dependencies → **waiting**
- `in-progress` or `in-review` → **in flight**
- `done` → complete
- `blocked` → flag immediately

If there are no available tasks and no in-flight tasks, the cycle is complete or fully blocked. Report and stop.

---

### 2 — Launch Implement Agents in Parallel

For each available task, launch one implement agent simultaneously following `engineering/implement.md`.

Each agent:
- Adopts the assigned team member persona
- Implements the task TDD
- Opens a PR
- Updates the task to `in-review`

Do not wait for one task to finish before starting another. Parallelise fully.

---

### 3 — Launch Review Agents as PRs Open

As each implement agent opens a PR, launch a review agent for it following `engineering/review.md`. Do not batch reviews — start each review as soon as the PR is ready.

Each review agent:
- Assembles the domain-appropriate review team
- Runs reviews in parallel
- Synthesises findings
- Approves or requests changes

If changes are requested: the implement agent addresses them and the review reruns. This loop continues until approval.

---

### 4 — Merge and Update

Once a PR is approved:
- Merge the PR
- Update the task status to `done` in BACKLOG.md
- Check if any waiting tasks are now unblocked (all dependencies `done`)

---

### 5 — Repeat

Return to Step 1. Pick up newly available tasks. Continue until the milestone is complete or all remaining tasks are blocked.

---

### 6 — Report

When the cycle ends, produce a build summary:

```
# Build Summary — [Milestone/Slice Name]

## Completed
- [Task N.N.N] [name] — merged

## In flight
- [Task N.N.N] [name] — in-review

## Blocked
- [Task N.N.N] [name] — blocked on [dependency or decision]

## Remaining
- [Task N.N.N] [name] — todo, available next cycle

## Next step
[All tasks done → run /qa | Tasks blocked → list what needs resolving | Tasks remaining → run /build again]
```
