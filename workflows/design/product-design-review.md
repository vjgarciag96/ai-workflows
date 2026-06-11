# Workflow: UX Design Review

## Purpose

Run a structured multi-perspective review of a completed design document. Surface gaps between the design and the PRD intent, missing states, spec ambiguities, and open questions. Drive the design document to a state where implementation can begin without guessing.

## Input

- `spec/design/DESIGN.md` — the design document to review
- `spec/product/PRD.md` — for context and intent

## Output

An updated `spec/design/DESIGN.md` with decisions documented and critical gaps closed. If any product decisions surface, `spec/product/PRD.md` is updated too.

---

## Principles

- Run all team members. Every role catches different things.
- Run independent reviewers in parallel — they must not see each other's reviews before writing their own.
- The goal is not to redesign. The goal is to find what an engineer would build wrong, what a user would experience badly, and what a spec leaves to guesswork.
- Synthesis is the most important step. Do not dump all reviews on the user — find the themes, the gaps, and the things multiple reviewers flagged independently.
- Distinguish design decisions (go in DESIGN.md) from product decisions (go in PRD) from implementation details (go in tech spec).
- Every decision the user makes gets written into the document before moving on.

---

## Steps

### 1 — Read the Design Document

Read `spec/design/DESIGN.md` and `spec/product/PRD.md` in full before launching any reviewers. Understand the screen inventory, state machine, component patterns, flows, and acceptance criteria.

---

### 2 — Run All Reviewers in Parallel

Launch one agent per team member simultaneously. Each agent receives DESIGN.md, PRD.md, and their character, role, and focus areas from `workflows/team/`.

**Do not let reviewers see each other's output at this stage.**

#### Design review focus by role

**McGonagall** — Missing states; spec completeness; trust moments; what "clear message" actually means as a spec; places where engineering will guess wrong if the document is silent.

**Dean** — What each screen concretely looks like; component behaviour; developer ambiguity; will an engineer build this wrong from the current description.

**Tonks** — Human moments; emotional experience of each wait and each decision; copy that misleads or over-promises; coordination gaps between roles where both sides have a different mental model.

**Percy** — Missing acceptance criteria; ambiguous states; deferred decisions the design exposes; places where "clear message" is stated as a requirement but not specified.

**Neville** — Missing edge case states; platform and device fragmentation risk in the UI layer; accessibility gaps; states the design assumes will never happen.

**Harry** — Android-specific design assumptions; permissions flow; what a junior developer will build wrong or need to look up; component choices that don't exist natively on Android.

**Hermione** — Design-to-backend contract; which screens assume data that requires specific API calls; state machine coverage in the screen flows; data the screens assume is available.

**Ginny** — What happens when backend data is unavailable; fallback states for missing or partial data; timing assumptions in the flows.

**Moody** — Social engineering vectors in the UI; misleading copy that lowers a user's guard; trust signals that could be spoofed; confirmation flows that can be bypassed.

**Arthur** — Operational states implied by the design; timing edge cases; states that require backend events the design doesn't name.

**Dumbledore** — Design decisions that constrain architecture before it is written; what must be decided before implementation begins; design choices that will be expensive to change later.

**Snape** — Instrumentation events implied by the design; what the current design makes measurable and what it leaves opaque; success criteria implied by specific screen states.

**Ron** — Browser-facing states and link handling before install; cross-platform design assumptions that will need to change for web.

**Sirius** — Components that will need to change for cross-platform support; platform-incompatible assumptions in the design; what a future cross-platform build would require rethinking.

**Luna** — What the design leaves on the table; the most interesting version of a flow that isn't being built; delight moments that could exist without adding scope.

**Colin** — Does the design tell the right success story; does the screen inventory match the stated problem; which flows feel like they solve a product need and which feel like filler.

**Fred** — Conversion moments in the design; post-interaction hooks; places where a user at peak engagement has nowhere to go.

**Voldemort** — The fundamental contradiction in the design; the assumption that will cause the product to fail; the screen nobody will use and the reason nobody talks about it.

Each reviewer: 200–300 words, in character. Concrete and specific.

---

### 3 — Synthesise

Do not present reviews individually. Instead:

**Group findings into themes** — e.g. "Missing states", "Spec gaps", "Copy issues", "Backend assumptions", "Android-specific risks"

**Identify cross-cutting issues** — things multiple reviewers flagged independently carry the most weight.

**Separate design decisions from product decisions from implementation details** — only design decisions go in DESIGN.md; product decisions go in PRD.

Present the synthesis to the user. Lead with critical issues, then important gaps, then debates worth having.

---

### 4 — Focused Back-and-Forth

For specific unresolved questions, bring 2–4 relevant team members into a focused discussion — not a re-review. Frame the question, include the user's position if they have one, have the characters debate, and land on a concrete recommendation.

---

### 5 — Capture Decisions and Update the Document

For every decision the user makes:
- Update DESIGN.md immediately
- Update PRD.md if a product decision surfaced
- Flag implementation details for the tech spec — do not let them creep into DESIGN.md

---

### 6 — Commit

Commit the updated document(s) with a message summarising what the design review decided.
