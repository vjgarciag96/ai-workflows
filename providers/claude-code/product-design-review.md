# Command: ux-design-review

Run a structured multi-perspective review of a completed design document. Surface missing states, spec gaps, developer ambiguities, and open questions. Drive the document to a state where implementation can begin without guessing.

**MANDATORY** Run all team members. Do not skip roles.
**MANDATORY** Run independent reviewers in parallel — they must not see each other's reviews before writing their own.
**MANDATORY** Do not dump all reviews on the user. Synthesise into themes, cross-cutting issues, and critical gaps.
**MANDATORY** Every decision the user makes gets written into DESIGN.md immediately.
**MANDATORY** Distinguish design decisions (DESIGN.md) from product decisions (PRD.md) from implementation details (tech spec).

---

## The Team

Defined in full in `team/` (one file per team member). Summary:

| Character | Role |
|---|---|
| Dumbledore | Principal Engineer |
| Hermione | Senior Backend Engineer |
| Ron | Senior Web Engineer |
| Sirius | Senior iOS Engineer |
| Luna | Creative PM |
| Percy | Conservative PM |
| McGonagall | Principal Designer |
| Snape | Data Scientist |
| Moody | Security Engineer |
| Neville | QA / Testing |
| Arthur | DevOps / SRE |
| Tonks | UX Researcher |
| Fred | Growth / Marketing |
| Harry | Junior Android Engineer |
| Ginny | Junior Backend Engineer |
| Colin | Junior PM / Product Analyst |
| Dean | Junior Designer |
| Voldemort | Adversarial Reviewer |

Victor (Senior Android Engineer) is the product owner. His decisions close the open questions the team surfaces.

---

## Step 1 — Read the Design Document

Read `spec/design/DESIGN.md` and `spec/product/PRD.md` in full before launching any reviewers. Understand the screen inventory, state machine, component patterns, flows, and acceptance criteria.

---

## Step 2 — Run All Reviewers in Parallel

Launch one agent per team member simultaneously. Each agent receives DESIGN.md, PRD.md, and their specific character, role, focus, and voice from the roster.

Design review focus per role:

- **McGonagall**: Missing states; spec completeness; trust moments; places where engineering will guess wrong if the document is silent
- **Dean**: What each screen concretely looks like; developer ambiguity; will an engineer build this wrong
- **Tonks**: Human moments; emotional experience; copy that misleads; coordination gaps between roles where both sides have a different mental model
- **Percy**: Missing acceptance criteria; ambiguous states; deferred decisions the design exposes
- **Neville**: Missing edge case states; platform and device fragmentation risk; accessibility gaps
- **Harry**: Android-specific design assumptions; permissions flow; what a junior dev will build wrong
- **Hermione**: Design-to-backend contract; data the screens assume is available; state machine coverage
- **Ginny**: Fallback states for missing or partial data; timing assumptions; what happens when backend data is unavailable
- **Moody**: Social engineering vectors in the UI; misleading copy; trust signals that could be spoofed
- **Arthur**: Operational states implied by the design; timing edge cases; backend events the design doesn't name
- **Dumbledore**: Design decisions that constrain architecture; what must be decided before implementation begins
- **Snape**: Instrumentation events implied by the design; what the design makes measurable or opaque
- **Ron**: Browser-facing states; link handling in the browser before install; cross-platform design assumptions
- **Sirius**: Components that will need to change for cross-platform; platform-incompatible assumptions
- **Luna**: What the design leaves on the table; the most interesting flow not being built
- **Colin**: Does the design tell the right success story; which flows solve a real need
- **Fred**: Conversion moments; post-interaction hooks; users at peak engagement with nowhere to go
- **Voldemort**: The fundamental contradiction; the assumption that will cause the product to fail

Each reviewer: 200–300 words, in character.

---

## Step 3 — Synthesise

Group findings into themes. Identify cross-cutting issues — multiple reviewers flagging the same thing independently carries the most weight. Separate design decisions from product decisions from implementation details.

Lead with critical issues, then important gaps, then debates worth having.

---

## Step 4 — Focused Back-and-Forth

For specific unresolved questions, bring 2–4 relevant team members into a focused discussion. Frame the question, have the characters debate, land on a concrete recommendation for the user to decide.

---

## Step 5 — Update the Documents

For every decision the user makes, update DESIGN.md immediately. If a product decision surfaced, update PRD.md too. Flag implementation details for the tech spec.

---

## Step 6 — Commit

Commit the updated document(s) with a message summarising what the design review decided.
