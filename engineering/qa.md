# Workflow: QA

## Purpose

Run a pre-release QA pass across a milestone or set of stories. Gates release, not merge. Neville leads. Any failures become new tasks in the backlog.

## Input

- A milestone, slice, or list of stories to QA
- `spec/engineering/BACKLOG.md` — for ACs
- `spec/product/PRD.md` — for user stories and product intent
- `spec/design/DESIGN.md` — for screen states and interaction behaviour
- The running application

## Output

- A QA report: passed ACs, failed ACs, and bugs found
- New tasks appended to BACKLOG.md for any failures
- A release sign-off, or a block with the list of failures that must be resolved first

---

## Principles

- QA does not gate merging. It gates release. Code merges continuously; QA runs before a milestone ships.
- Neville leads but does not work alone. Each story's domain owner joins QA for that story — they know what can go wrong.
- Every AC in scope must be checked. Unchecked ACs are not passed ACs.
- Bugs found during QA become tasks in the backlog immediately. They do not block the rest of QA unless they make other checks impossible.
- Edge cases are first-class. The happy path is the least interesting thing to check.
- Device and platform variation is explicitly tested, not assumed to work because the simulator passed.

---

## Steps

### 1 — Read the Scope

Read BACKLOG.md. Identify the stories and tasks in scope for this QA pass. Confirm all tasks are `done` (merged). Any `in-progress` or `in-review` tasks are out of scope — note them.

---

### 2 — Assemble the QA Team

Neville leads every session.

For each story in scope, add the domain-primary team member for that story's tasks:
- Android stories → Harry
- Backend stories → Hermione
- Infra stories → Arthur

Moody joins any story touching auth, permissions, or user data.

---

### 3 — Run QA by Story

For each story in scope:

**Read:** the story's ACs from BACKLOG.md and the corresponding user stories from PRD.md.

**Check each AC:**
- Happy path: does the feature work as specified?
- Failure paths: do error states behave as designed?
- Edge cases: connectivity loss, process death, concurrent state changes, platform variation
- Design fidelity: does the UI match DESIGN.md? Check specific screen states, copy, and component behaviour.

**Log the result for each AC:** `pass` | `fail` | `blocked` (cannot check due to a dependency)

**For each failure:** write a bug description with:
- Which AC failed
- Steps to reproduce
- Expected behaviour (from ACs / DESIGN.md)
- Actual behaviour
- Severity: `critical` (release blocker) | `major` (significant but workaroundable) | `minor` (cosmetic or edge case)

---

### 4 — Append Bugs to Backlog

For each bug found, append a new task to the relevant story in BACKLOG.md:

```
#### Task N.N.N: Fix [bug description]
**Owner:** [domain-appropriate team member]
**Domain:** [domain]
**Status:** todo
**Dependencies:** none
**Severity:** critical | major | minor
**ACs:**
- [ ] [the failing AC, restated as a fix criterion]
```

---

### 5 — Produce QA Report

Summarise the QA pass:

```
# QA Report — [Milestone/Slice Name]

## Summary
- Stories checked: N
- ACs checked: N
- Passed: N
- Failed: N (N critical, N major, N minor)
- Blocked: N

## Failures
[list of failed ACs with bug task references]

## Sign-off
[APPROVED FOR RELEASE | BLOCKED — list of critical failures that must be resolved]
```

---

### 6 — Commit

Commit the updated BACKLOG.md (new bug tasks appended) and the QA report.
