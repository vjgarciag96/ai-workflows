# Workflow: Tech Spec

## Purpose

Take a signed-off PRD and design document and produce a complete technical specification — before any implementation code is written.

The workflow has two phases: a pre-spec review that surfaces architectural decisions, and a post-spec review that validates the full document. Decisions from either phase that affect the product or design are written back to those documents immediately.

## Input

- `spec/product/PRD.md` — the signed-off PRD
- `spec/design/DESIGN.md` — the signed-off design document
- `spec/design/prototype.html` — the interactive prototype, if available

## Output

- `spec/engineering/TECH_SPEC.md` — the full technical specification
- `spec/product/PRD.md`, updated with any product decisions surfaced during the engineering phase
- `spec/design/DESIGN.md`, updated with any design decisions surfaced during the engineering phase

---

## Principles

- **Engineering drives spec, not the other way around.** Let the team surface architectural questions before writing a word of the spec. Writing first and reviewing second embeds assumptions that are expensive to undo.
- **Two phases, two purposes.** Phase 1 (pre-spec) surfaces decisions. Phase 2 (post-spec) validates the document. These are different questions and should not be conflated.
- **Decisions are hierarchical.** Product decisions go in the PRD. Design decisions go in DESIGN.md. Implementation decisions go in the tech spec. Do not let implementation details creep up or product decisions stay buried in a tech spec.
- **Issues flagged by multiple reviewers independently carry the most weight.** The synthesis step is where this signal is extracted.
- **The tech spec must be complete enough that implementation can begin without guessing.** If an engineer would have to make a decision that isn't in the spec, that decision belongs in the spec.
- **Independent reviewers must not see each other's output before writing their own.** Run in parallel.

---

## Steps

### 1 — Read the Inputs

Read PRD.md and DESIGN.md in full. Understand the session state machine, user stories, screen inventory, and known risks before launching any reviewers.

---

### 2 — Pre-Spec Engineering Review

Launch one agent per engineer simultaneously. Each agent receives the PRD, the design document, and their character, role, and focus from `team/`.

**Do not let reviewers see each other's output at this stage.**

The goal is not a full review — it is surfacing the decisions that must be made before the spec is written. Each reviewer should identify:

- Architectural choices the spec must commit to
- Ambiguities in the PRD/design that will force a decision mid-implementation
- Risks specific to their domain that should shape the spec's structure
- Questions the team must resolve before writing begins

**Engineering pre-spec team:**

- **Dumbledore** (Principal Engineer) — overall architecture; constraints that shape every other decision; what must be committed to now vs. deferred safely; choices that will be expensive to reverse
- **Hermione** (Senior Backend Engineer) — backend architecture; data model; session state machine; client-server trust; API surface; what the client must not be trusted to send
- **Harry** (Junior Android Engineer) — SDK and library choices; Android-specific constraints; permissions and platform requirements; what a junior developer will get wrong or need guidance on
- **Arthur** (DevOps / SRE) — infrastructure implied by the design; scaling and failure modes; operational requirements; what happens when the service is unavailable
- **Moody** (Security Engineer) — attack vectors; credential handling; trust surfaces in the protocol; what the security model must commit to before the spec is written
- **Neville** (QA / Testing) — connectivity loss; app lifecycle edge cases; platform and device fragmentation; states the design assumes will never happen but will

Each reviewer: 300–500 words, in character, specific to their domain. Not a general review — a targeted list of decisions the spec must make.

---

### 3 — Synthesise Pre-Spec Findings

Group findings into themes. Identify decisions flagged by multiple reviewers independently. Separate:

- Architectural decisions that must be made before writing begins
- Product decisions that need to go back to the product owner (and into the PRD)
- Design decisions that need to go back into DESIGN.md

Present to the product owner. For each open question: what the question is, why it matters now, what the options are.

---

### 4 — Resolve Pre-Spec Questions

For each open question, get a decision from the product owner. Do not write the spec until architectural questions are resolved.

Write every decision that affects the product into the PRD immediately. Write every decision that affects the design into DESIGN.md immediately. Commit the updated documents before proceeding.

---

### 5 — Write the Tech Spec

Write `spec/engineering/TECH_SPEC.md`.

**Required sections:**

1. **Overview** — what this document covers; what it does not cover; relationship to PRD and design doc
2. **Architecture** — system components and their responsibilities; data flow; what lives where
3. **State Machine** — the authoritative state diagram with every state, every transition, and every trigger; must be more detailed than the PRD version
4. **Protocol / Signalling** — every message type, direction, payload, and error case for real-time communication
5. **Client** — per platform in scope; platform-specific service and permission model; key SDK and library choices with rationale
6. **Backend** — each service or module; data model; storage schema; TTL handling; deployment requirements
7. **Transport / Media** — communication protocol; connection model; data channel design
8. **Security** — auth; token lifecycle; trust surfaces; what the server must verify; what the client must not be trusted to send
9. **Platform / Edge Cases** — known fragmentation risks; fallbacks; degraded modes
10. **API Reference** — every endpoint; request/response schemas; error codes
11. **Observability** — metrics; alerts; what must be monitored and at what threshold
12. **Open Questions** — explicitly named; deferred to post-MVP only if safe to defer

The spec must be complete enough that an engineer can implement from it without making undocumented decisions. If a threshold, timeout, or value matters, it must be in the spec.

---

### 6 — Post-Spec Review

Launch one agent per team member simultaneously. Each agent receives the tech spec, the PRD, and the design document, plus their character and role. Run in parallel.

**Do not let reviewers see each other's output at this stage.**

#### Tech spec review focus by role

- **Dumbledore** — architecture coherence; decisions that will be expensive to reverse; what is missing at the architectural level
- **Hermione** — backend correctness; state machine completeness; API contract; trust surfaces; what the server accepts that it should not
- **Harry** — Android implementation correctness; SDK and platform specifics; permissions; what a junior developer will build wrong from this spec
- **Arthur** — infrastructure gaps; operational requirements implied but not stated; failure modes not addressed; monitoring and alerting coverage
- **Moody** — security model completeness; attack vectors the spec leaves open; credential handling; replay attacks; social engineering vectors
- **Neville** — edge case coverage; connectivity loss handling; platform and device fragmentation; app lifecycle; states the spec assumes will never occur
- **Percy** — missing acceptance criteria; ambiguous thresholds; implementation details left to guesswork; deferred decisions that are not safe to defer
- **Ginny** — client-server protocol detail; retry behaviour; what happens when backend is slow or unavailable; race conditions in the protocol
- **Ron** — web components; anything the spec implies about the browser-side experience
- **Snape** — observability; what the spec makes measurable and what it leaves opaque; success metrics implied by specific states
- **Sirius** — decisions that would foreclose future iOS support; cross-platform assumptions
- **Luna** — what the spec leaves on the table; the most interesting version of the architecture not being built
- **McGonagall** — design-to-spec contract; whether the spec covers every screen state in the design
- **Colin** — does the spec match the product intent; does it solve the right problem at the right level
- **Fred** — post-interaction hooks implied by the architecture; anything the spec enables or forecloses for growth
- **Dean** — spec-to-implementation handoff; what a designer would catch that engineers overlook
- **Tonks** — human experience implied by the protocol choices; latency and responsiveness constraints; where the spec will make the experience feel broken
- **Voldemort** — the assumption at the core of the spec that will cause the implementation to fail; the decision nobody has questioned

Each reviewer: 200–300 words, in character, concrete and specific.

---

### 7 — Synthesise Post-Spec Findings

Group findings into themes. Identify issues flagged by multiple reviewers independently. Separate:

- Errors (the spec is wrong)
- Gaps (the spec is silent on something that matters)
- Product decisions that should go back to the product owner
- Debates worth having (no clear right answer, but worth discussing)

Present the synthesis. Lead with errors, then gaps, then debates. Do not present individual reviews.

---

### 8 — Resolve and Apply

For each issue the product owner decides to address:

- Update TECH_SPEC.md immediately
- Update PRD.md if a product decision surfaced
- Update DESIGN.md if a design decision surfaced

For items deferred, name them explicitly in the spec's Open Questions section.

---

### 9 — Commit

Commit the updated spec and any updated documents together. The commit message should summarise what the review phase decided — not just "updated spec."
