# Workflow: UX Design

## Purpose

Take a signed-off PRD and produce an interactive HTML prototype covering every screen, every state, and every critical interaction — before a line of implementation code is written.

## Input

A `spec/product/PRD.md` file.

## Output

- `spec/design/prototype.html` — a self-contained, interactive HTML/CSS/JS prototype. Mobile viewport, phone frame, dev nav for jumping to any screen/state. No external dependencies.
- `spec/design/DESIGN.md` — the engineering-facing design specification. Covers every screen, every state, every component, every interaction pattern, copy guidelines, and what is deferred to the tech spec. This is what engineers build against; the prototype is the visual reference.
- `spec/product/PRD.md`, updated with every product decision surfaced during the design phase.

---

## Principles

- The prototype is the artefact, not a design tool. It lives in the repo and is what you build against.
- A screen inventory is not enough. You need navigable states — loading, error, edge case, trust moment — not just happy path.
- Every open question the designers surface is a product decision. It goes back to the product owner and, once decided, into the PRD.
- Build the prototype directly — no subagents, no external tools. Write the HTML/CSS/JS yourself.
- Single HTML file, no external dependencies. Anyone can open it.
- The dev nav is the screen inventory. Every screen and state is reachable from it.
- Designers run in parallel and independently — they should not see each other's output before writing their own.

---

## Steps

### 1 — Read the PRD

Read the PRD in full before launching any designers. Understand the session state machine, user stories, and known risks.

---

### 2 — Run All Designers in Parallel

Launch one agent per designer simultaneously. Each agent receives the full PRD and their character, role, focus, and voice.

**Design team:**

- **McGonagall** (Principal Designer) — every screen and every state, including failures; high-stakes trust moments; what "clear message" actually means as a spec; the experience of waiting and uncertainty
- **Dean** (Junior Designer) — what it looks like on screen; how the product's core model resolves visually; the primary working state; destructive mechanics; status states visually
- **Tonks** (UX Researcher) — friction; first-time experience for each role; emotional experience of key waits and blocked states; mental models; the trust moment

Each reviewer: 300–500 words, in character, concrete and specific. "Clear message" is not a design spec.

**Do not let designers see each other's output at this stage.**

---

### 3 — Synthesise

Combine the three reviews into:

1. **Screen inventory** — every screen and every state, named. Cross-reference what multiple designers flagged independently — those carry the most weight.
2. **Open questions** — decisions the PRD does not answer that the prototype would expose. Present these to the product owner concisely — what the question is, why it matters, what the options are.

Do not present three separate reviews. Synthesise.

---

### 4 — Resolve Open Questions

For each open question, present it to the product owner and get a decision. Do not proceed to prototype until all questions are resolved.

Every decision made here must be written into the PRD immediately — user stories, key product decisions table, or MVP scope as appropriate.

---

### 5 — Build the Prototype

Build `design/prototype.html` directly. Requirements:

**Structure**
- Single self-contained HTML file — no external dependencies, no CDN imports
- Mobile phone frame (390×844px) centered in the browser viewport with a device bezel
- Dev nav above the phone frame — buttons to jump to every screen and sub-state directly
- Real status bar at the top of the phone showing the current time

**Coverage**
- Every screen from the screen inventory
- Every sub-state reachable via the dev nav
- Working timers (countdowns, session duration) using `setInterval`
- Confirmation dialogs before destructive actions
- Toast notifications for feedback

**Visual style**
- Clean, material-design-adjacent — this is an Android app
- CSS custom properties for the colour palette
- Rounded corners, generous padding, clear type hierarchy
- No wireframe aesthetic — it should look like a real app

**What not to do**
- Do not use any external font, icon, or CSS library
- Do not write a `screens.md` separately — the dev nav is the screen index
- Do not skip error states, loading states, or edge cases to save time

---

### 6 — Write DESIGN.md

After the prototype is complete, write `spec/design/DESIGN.md` — the engineering-facing design specification.

This document must cover:
- **Design system:** full color palette (CSS token names and hex values), typography scale, layout constants
- **Navigation model:** tab bar, app bar, status bar — structure and behaviour
- **Screen inventory:** for every screen and every sub-state — layout, all UI elements with sizes/weights/colors, and interactions
- **Overlays and sheets:** every bottom sheet, scrim, and toast — triggers, content, dismissal rules
- **Interaction patterns:** the key flows (status change, add from search, remove, offline, sync conflict) described step-by-step
- **Copy guidelines:** exact strings for all system messages, banners, empty states, and confirmation dialogs; copy principles
- **What this design defers:** implementation details explicitly out of scope (data sources, sync protocol, token storage, etc.)

The prototype is the visual reference. DESIGN.md is what an engineer reads to understand every decision without opening the prototype.

---

### 7 — Commit

Commit the prototype, DESIGN.md, and the updated PRD together with a message describing what the design phase decided.
