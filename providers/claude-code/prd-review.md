# Command: prd-review

Run a structured multi-perspective review of a PRD using the full team roster. Surface critical issues, debates, and open questions. Drive the PRD to a state where implementation can begin.

**MANDATORY** Run all team members. Do not skip roles.
**MANDATORY** Run independent reviewers in parallel — they must not see each other's reviews before writing their own.
**MANDATORY** Do not dump all reviews on the user. Synthesise into themes, debates, and critical issues.
**MANDATORY** Every decision the user makes gets written into the PRD immediately.
**MANDATORY** Distinguish product decisions (PRD) from implementation details (tech spec).

---

## The Team

Defined in full in `workflows/team/` (one file per team member). Summary:

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

## Step 1 — Read the PRD

Read the full PRD before launching any reviewers.

---

## Step 2 — Run All Reviewers in Parallel

Launch one agent per team member simultaneously. Each agent receives the full PRD and their specific character, role, focus, and voice from the roster.

PRD review focus per role:

- **Dumbledore**: Architectural decisions implied but not made; what must be decided before code is written; long-term implications
- **Hermione**: Backend infrastructure; state machine completeness; authentication and token design; data model
- **Ron**: Web-related deferred decisions; what the product does in a browser; transport choices affecting future web
- **Sirius**: Platform expansion claims; what cross-platform support means per role; decisions that foreclose other platforms
- **Luna**: Assumptions worth questioning; the most interesting version of the product; the magic moment
- **Percy**: Ambiguous stories; missing acceptance criteria; deferred decisions that must be made now; success criteria
- **McGonagall**: All states including failure paths; what "clear message" means as a design spec; high-stakes trust moments
- **Snape**: Success metrics; instrumentation events; qualitative goals in measurable terms
- **Moody**: Attack vectors; credentials and token security; encryption; abuse surfaces; social engineering
- **Neville**: Edge cases; connectivity loss; app lifecycle; mid-interaction states; platform fragmentation
- **Arthur**: Infrastructure implied; real-time coordination requirements; scaling; failure modes; observability
- **Tonks**: First-time experience; onboarding friction; who is harder to bring in; mental models
- **Fred**: Viral loops; acquisition; hook moment; retention; role-switching and conversion moments
- **Harry**: Things seniors assume away; Android-specific questions; first screen; what the app actually looks like
- **Ginny**: Client-server trust model; API and URL surface exposure; data retention; retry ceilings
- **Colin**: The success story; problem framing precision; who takes the first step; what brings someone back
- **Dean**: What it actually looks like; state communication in UI; the primary working state; destructive mechanics
- **Voldemort**: The premise; contradictions between stated goals; the one assumption that kills the product if wrong

Each reviewer: 200–300 words, in character.

---

## Step 3 — Synthesise

Group findings into themes. Identify issues flagged by multiple reviewers independently — these carry the most weight. Name the debates. Separate product decisions from implementation details.

Lead with critical issues, then important gaps, then debates worth having.

---

## Step 4 — Focused Back-and-Forth

For specific unresolved questions, bring 2–4 relevant team members into a focused discussion. Frame the question, include the user's initial position if they have one, have the characters debate, and land on a concrete recommendation for the user to decide.

---

## Step 5 — Update the PRD

For every decision the user makes, update the PRD immediately. Add to Key Product Decisions where appropriate. Flag implementation details for the tech spec.

---

## Step 6 — Commit

Commit the updated PRD with a message summarising what changed.
