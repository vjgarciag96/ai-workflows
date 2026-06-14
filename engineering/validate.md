# Workflow: Validate

## Purpose

Check that the implementation matches the spec and design at a milestone level. Where QA checks ACs feature by feature, validation checks fidelity to the architecture, API contracts, and design document holistically. Produces a gap list — either closes the milestone or generates remediation tasks.

## Input

- `spec/engineering/TECH_SPEC.md`
- `spec/product/PRD.md`
- `spec/design/DESIGN.md`
- `spec/engineering/BACKLOG.md`
- The codebase

## Output

- A validation report: gaps found, remediation tasks, and milestone sign-off or block
- New tasks appended to BACKLOG.md for any gaps
- Updated milestone status

---

## Principles

- Validation is not QA. QA checks ACs feature by feature. Validation checks whether the whole is coherent — architecture, contracts, design fidelity, and product intent together.
- The spec is the authority. If the implementation diverges from the spec, that is a gap — unless the spec was explicitly updated to reflect a decision made during implementation. Undocumented divergence is always a gap.
- Gaps are not always bugs. Sometimes the spec needs to be updated to reflect a better decision made during implementation. The validator's job is to surface the divergence, not to always revert to the spec.
- Run validators in parallel and independently.

---

## Steps

### 1 — Read the Inputs

Read TECH_SPEC.md, PRD.md, DESIGN.md, and BACKLOG.md in full. Understand what was planned before reading what was built.

---

### 2 — Run Validators in Parallel

Launch one agent per validator simultaneously. Each receives all spec documents, their character from `team/`, and access to the codebase.

**Do not let validators see each other's output at this stage.**

- **Dumbledore** — architecture fidelity: does the implementation match the system architecture in TECH_SPEC.md? Component responsibilities, data flow, failure domains. Flag any structural divergence.

- **Hermione** — API and state machine fidelity: do the implemented endpoints match the API reference? Are all state transitions implemented? Are error codes correct? Is the data model as specified?

- **McGonagall** — design fidelity: is every screen state in DESIGN.md implemented? Does the copy match? Do component behaviours match the acceptance criteria in the design doc? Check edge states, not just happy path.

- **Percy** — AC completeness: are all story-level ACs in BACKLOG.md met? Are any marked done that aren't demonstrably complete? Are any ACs missing from the backlog that the PRD implies?

- **Moody** — security fidelity: is the security model in TECH_SPEC.md implemented correctly? Token handling, permission checks, trust surfaces. Any deviation from the spec is a gap.

Each validator: 300–500 words. A concrete list of gaps with spec references — not a general review.

---

### 3 — Synthesise

Group gaps by type:
- **Implementation gaps** — the spec says X, the code does Y
- **Spec gaps** — the implementation made a reasonable choice the spec didn't cover; spec should be updated
- **Design gaps** — a screen state or interaction is missing or wrong
- **AC gaps** — a user story from the PRD has no coverage in the backlog

For each gap, recommend: fix the implementation, update the spec, or acknowledge as a known deviation.

Present to the product owner. Get a decision on each gap before writing tasks.

---

### 4 — Append Remediation Tasks to Backlog

For each gap the product owner decides to fix, append a task to BACKLOG.md:

```
#### Task N.N.N: [gap description]
**Owner:** [appropriate team member]
**Domain:** [domain]
**Status:** todo
**Dependencies:** none
**Gap type:** implementation | spec | design | ac
**ACs:**
- [ ] [what done looks like for this gap]
```

For gaps resolved by updating the spec or design doc, make those updates immediately and note them in the validation report.

---

### 5 — Produce Validation Report

```
# Validation Report — [Milestone/Slice Name]

## Summary
- Implementation gaps: N
- Spec gaps: N
- Design gaps: N
- AC gaps: N
- Remediation tasks created: N
- Spec/design updates made: N

## Gaps
[list of gaps with decisions]

## Sign-off
[MILESTONE VALIDATED | BLOCKED — list of gaps that must be resolved first]
```

---

### 6 — Commit

Commit the updated BACKLOG.md, any updated spec/design documents, and the validation report together.
