# Command: ux-design

Take a signed-off PRD and produce an interactive HTML prototype covering every screen, every state, and every critical interaction — before any implementation code is written.

**MANDATORY** Run all designers in parallel. Do not skip any.
**MANDATORY** Every open question gets resolved with the product owner before the prototype is built.
**MANDATORY** Every decision ripples back into the PRD immediately.
**MANDATORY** Build the prototype directly — write the HTML/CSS/JS yourself. No subagents, no external tools.
**MANDATORY** Single self-contained HTML file. No external dependencies.

---

## The Design Team

| Character | Role | Focus |
|---|---|---|
| McGonagall | Principal Designer | Every screen and state including failures; high-stakes trust moments; what "clear message" actually means as a spec |
| Dean | Junior Designer | What it looks like on screen; how the product's core model resolves visually; the primary working state; destructive mechanics; status states visually |
| Tonks | UX Researcher | Friction; first-time experience for each role; emotional experience of key waits and blocked states; mental models; the trust moment |

Each reviewer: 300–500 words, in character. Concrete and specific. "Clear message" is not a design spec.

---

## Step 1 — Read the PRD

Read the PRD in full. Understand the state machine, user stories, and known risks before launching designers.

---

## Step 2 — Run All Designers in Parallel

Launch McGonagall, Dean, and Tonks simultaneously. Each receives the full PRD plus their character definition from `workflows/team/`. They must not see each other's output at this stage.

**McGonagall** — produce a complete screen inventory: every screen, every state, every trust and error moment. Named and described specifically.

**Dean** — describe what the app actually looks like. Dual-role entry point. Each screen step by step. The floating overlay. Status states visually. Flag anything that doesn't resolve when you try to actually picture it.

**Tonks** — identify where real people will get confused, frustrated, or give up. Name the emotions. Describe what a real person thinks and feels at each friction point. Surface the design decisions this forces.

---

## Step 3 — Synthesise

Produce:

1. **Screen inventory** — every screen and sub-state, named. Issues flagged by multiple designers independently carry the most weight.
2. **Open questions list** — decisions the PRD doesn't answer that the prototype would expose. Concise: what the question is, why it matters, what the options are.

Present to the product owner.

---

## Step 4 — Resolve Open Questions

Get a decision on each open question. Do not build until all are resolved.

Write every decision into the PRD immediately — user stories, key product decisions table, or MVP scope as appropriate.

---

## Step 5 — Build the Prototype

Save to `spec/design/prototype.html`.

**Requirements:**
- Single HTML file, no external dependencies
- 390×844px phone frame with bezel, centered in viewport
- Dev nav above the frame — jump to every screen and sub-state directly
- Every state from the screen inventory reachable via dev nav
- Working timers (countdowns, session duration, grace windows) using `setInterval`
- Confirmation dialogs before destructive actions
- Toast notifications for user feedback
- Real clock in the status bar
- Material-design-adjacent visual style using CSS custom properties
- Looks like a real Android app — not a wireframe

Do not skip error states, loading states, or edge cases.

---

## Step 6 — Commit

Commit `design/prototype.html` and the updated `PRD.md` together. Message summarises what the design phase decided.
