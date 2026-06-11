# Workflow: PRD Review

## Purpose

Run a structured multi-perspective review of a PRD using the full team defined in `workflows/team/`. Surface critical issues, debates, and open questions. Drive the PRD to a state where implementation can begin.

## Input

A `spec/product/PRD.md` file.

## Output

An updated, improved `spec/product/PRD.md` with decisions documented and critical gaps closed.

---

## Principles

- Run all team members. Every role catches different things.
- Run independent reviewers in parallel — they should not see each other's reviews before writing their own.
- Junior voices ask what seniors have stopped asking. Do not skip them.
- Voldemort reviews last, or separately — his job is to attack the conclusions, not participate in the discussion.
- Synthesis is the most important step. Do not dump 15 reviews on the user — find the themes, the debates, and the things multiple people flagged independently.
- Back-and-forth on specific topics (not full re-reviews) is how decisions get made. Bring the right people into a focused discussion, not the whole room.
- Every decision the user makes gets written into the PRD before moving on.
- Distinguish product decisions (go in the PRD) from implementation details (go in the tech spec).

---

## Steps

### 1 — Read the PRD

Read the PRD in full before launching any reviewers.

---

### 2 — Run All Reviewers in Parallel

Launch one agent per team member simultaneously. Each agent receives:
- The full PRD text
- Their character, role, and focus areas (from the roster)
- Their specific review focus for this document type (see below)

**Do not let reviewers see each other's output at this stage.**

#### PRD review focus by role

**Dumbledore** — Architectural decisions implied but not made; what must be decided before code is written; long-term implications of choices being made now.

**Hermione** — Backend infrastructure implied; state machine completeness; API and data model questions; authentication and token design.

**Ron** — Web-related decisions deferred; what the product does in a browser; transport choices that affect future web support.

**Sirius** — Platform expansion claims; what cross-platform support actually means per role; decisions made now that foreclose other platforms later.

**Luna** — Assumptions worth questioning; the most interesting version of the product being left on the table; what would make this magical.

**Percy** — Ambiguous user stories; missing acceptance criteria; deferred decisions that must be made now; success criteria.

**McGonagall** — All states (not just happy path); what "clear message" means as a design spec; high-stakes trust moments; critical interaction flows.

**Snape** — Success metrics; instrumentation; what qualitative goals mean in measurable terms; what the account model costs analytically.

**Moody** — Attack vectors; credentials and token security; encryption; abuse surfaces; social engineering scenarios; what makes this product a tool for bad actors.

**Neville** — Edge cases; failure modes; connectivity loss; app lifecycle; mid-interaction states; missing acceptance criteria; platform fragmentation.

**Arthur** — Infrastructure implied; real-time coordination requirements; scaling; operational failure modes; latency SLOs; observability gaps.

**Fred** — Viral loops; acquisition; the hook moment; retention; role-switching and conversion moments; distribution.

**Harry** — Things seniors assume away; Android-specific questions (permissions, background behaviour, platform constraints); the first screen; what the app actually looks like.

**Ginny** — Trust model between client and server; what the API surface exposes; data retention; retry ceilings; the question Hermione would answer in five minutes.

**Colin** — The success story; precision of the problem framing; who takes the first step; what brings someone back; the first screen.

**Dean** — What it actually looks like; state communication in the UI; the primary working state; destructive mechanics.

**Voldemort** — The premise; contradictions between stated goals; the one assumption that kills the product if wrong; what the competitive landscape says about this product's chances.

---

### 3 — Synthesise

Do not present 17 individual reviews. Instead:

**Group findings into themes** — e.g. "Infrastructure / session model", "UX / first-time experience", "Security", "Scope and success criteria"

**Identify cross-cutting issues** — things multiple reviewers flagged independently carry more weight than individual opinions.

**Name the debates** — where reviewers would disagree (e.g. Luna vs Percy on scope, Moody vs Percy on approval friction), surface the tension explicitly.

**Separate product decisions from implementation details** — only product decisions go in the PRD.

Present the synthesis to the user. Do not overwhelm — lead with the critical issues, then the important gaps, then the debates worth having.

---

### 4 — Focused Back-and-Forth on Open Questions

For specific unresolved questions, bring the relevant team members into a focused discussion — not a re-review. Frame each discussion with:
- The question being debated
- The user's initial position if they have one
- Which team members are most relevant (2–4 people, not the whole room)

Have the characters debate and land on a concrete recommendation. Present it to the user for a decision.

---

### 5 — Capture Decisions and Update the PRD

For every decision the user makes:
- Update the relevant section of the PRD immediately
- Add to Key Product Decisions if it's a meaningful choice with a rationale
- Note anything explicitly deferred to the tech spec
- Do not let implementation details creep into the PRD

---

### 6 — Commit

Once the user is satisfied with the updated PRD, commit with a descriptive message summarising what changed.
