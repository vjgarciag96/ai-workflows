# Command: tech-spec

Take a signed-off PRD and design document and produce a complete technical specification. Two phases: a pre-spec engineering review that surfaces architectural decisions before writing begins, then a post-spec full-team review that validates the document.

**MANDATORY** Run all pre-spec reviewers in parallel. Do not start writing until architectural questions are resolved.
**MANDATORY** Run all post-spec reviewers in parallel. Do not let reviewers see each other's output.
**MANDATORY** Do not dump all reviews on the user. Synthesise into themes and decisions.
**MANDATORY** Every decision the user makes gets written into the relevant document immediately — PRD, DESIGN.md, or TECH_SPEC.md as appropriate.
**MANDATORY** Decisions are hierarchical: product decisions go in the PRD, design decisions go in DESIGN.md, implementation decisions go in the tech spec.

---

## Inputs

- `spec/product/PRD.md`
- `spec/design/DESIGN.md`
- `spec/design/prototype.html` (if available)

## Output

- `spec/engineering/TECH_SPEC.md`
- Updated `spec/product/PRD.md` and `spec/design/DESIGN.md` if product or design decisions surface

---

## Phase 1 — Pre-Spec Engineering Review

### Step 1 — Read the Inputs

Read PRD.md and DESIGN.md in full before launching reviewers.

### Step 2 — Run Pre-Spec Reviewers in Parallel

Six engineering-focused reviewers. Each receives the PRD, DESIGN.md, and their character from `workflows/team/`. Goal: surface the decisions that must be made before the spec is written, not a full review.

| Character | Role | Pre-spec focus |
|---|---|---|
| Dumbledore | Principal Engineer | Architecture; constraints; decisions expensive to reverse |
| Hermione | Senior Backend Engineer | Data model; state machine; client-server trust; API surface |
| Harry | Junior Android Engineer | SDK/library choices; Android permissions; foreground services; what a junior will get wrong |
| Arthur | DevOps / SRE | Infrastructure implied; scaling; failure modes; operational requirements |
| Moody | Security Engineer | Attack vectors; credential handling; trust surfaces; what must be committed to now |
| Neville | QA / Testing | Connectivity loss; app lifecycle; OEM fragmentation; states the design assumes never happen |

Each reviewer: 300–500 words, in character. A targeted list of decisions the spec must make — not a general review.

### Step 3 — Synthesise Pre-Spec Findings

Group by theme. Identify what multiple reviewers flagged independently. Separate: architectural decisions (must resolve before writing), product decisions (back to PRD), design decisions (back to DESIGN.md).

Present open questions to the user: what the question is, why it matters now, what the options are.

### Step 4 — Resolve Pre-Spec Questions

Get a decision on each open question. Write product decisions into the PRD and design decisions into DESIGN.md immediately. Commit before writing the spec.

---

## Phase 2 — Write the Tech Spec

### Step 5 — Write TECH_SPEC.md

Save to `spec/engineering/TECH_SPEC.md`.

**Required sections:**

1. **Overview** — scope, relationship to PRD and design doc
2. **Architecture** — components, responsibilities, data flow
3. **Session State Machine** — every state, transition, trigger; more detailed than the PRD version
4. **Signalling Protocol** — every message type, direction, payload, error case
5. **Android Client** — per role; foreground services; permissions; SDK choices with rationale
6. **Backend** — services; data model; storage schema; TTL handling; deployment requirements
7. **P2P / Media** — WebRTC config; ICE/STUN/TURN; codec chain; DataChannel design
8. **Security** — auth; token lifecycle; trust surfaces; what the server must verify
9. **OEM / Edge Cases** — fragmentation risks; fallbacks; degraded modes
10. **API Reference** — every endpoint; request/response schemas; error codes
11. **Observability** — metrics; alerts; thresholds
12. **Open Questions** — explicitly named; deferred only if safe to defer

Every threshold, timeout, and value that matters must be in the spec. If an engineer would have to make an undocumented decision, that decision is missing.

---

## Phase 3 — Post-Spec Review

### Step 6 — Run All Reviewers in Parallel

Full team. Each receives TECH_SPEC.md, PRD.md, and DESIGN.md, plus their character from `workflows/team/`.

**Do not let reviewers see each other's output.**

| Character | Role | Post-spec focus |
|---|---|---|
| Dumbledore | Principal Engineer | Architecture coherence; irreversible decisions; missing architectural coverage |
| Hermione | Senior Backend Engineer | Backend correctness; state machine completeness; API contract; trust surfaces |
| Harry | Junior Android Engineer | Android implementation; SDK specifics; what a junior builds wrong from this spec |
| Arthur | DevOps / SRE | Infrastructure gaps; failure modes; monitoring and alerting coverage |
| Moody | Security Engineer | Security model; attack vectors; credential handling; replay attacks |
| Neville | QA / Testing | Edge case coverage; connectivity loss; OEM fragmentation; lifecycle states |
| Percy | Conservative PM | Missing acceptance criteria; ambiguous thresholds; unsafe deferrals |
| Ginny | Junior Backend Engineer | Protocol detail; retry behaviour; race conditions; backend unavailability |
| Ron | Senior Web Engineer | Web components; browser-side implications |
| Snape | Data Scientist | Observability; what the spec makes measurable; success metrics |
| Sirius | Senior iOS Engineer | Decisions that foreclose future iOS support |
| Luna | Creative PM | What the spec leaves on the table; the most interesting architecture not being built |
| McGonagall | Principal Designer | Design-to-spec contract; spec coverage of every screen state |
| Colin | Junior PM / Product Analyst | Spec-to-product alignment; whether it solves the right problem |
| Fred | Growth / Marketing | Post-session hooks; what the architecture enables or forecloses for growth |
| Dean | Junior Designer | Spec-to-implementation handoff; what designers catch that engineers overlook |
| Tonks | UX Researcher | Latency and responsiveness; where protocol choices make the experience feel broken |
| Voldemort | Adversarial Reviewer | The assumption at the core of the spec that will cause the implementation to fail |

Each reviewer: 200–300 words, in character, concrete and specific.

### Step 7 — Synthesise Post-Spec Findings

Group by theme. Lead with: errors (spec is wrong), then gaps (spec is silent), then debates. Cross-reference independent flags — those carry the most weight. Do not present individual reviews.

### Step 8 — Resolve and Apply

For each decision: update TECH_SPEC.md, PRD.md, or DESIGN.md as appropriate. Defer only what is explicitly safe to defer, and name it in Open Questions.

### Step 9 — Commit

Commit all updated documents together. The commit message summarises what the review phase decided.
