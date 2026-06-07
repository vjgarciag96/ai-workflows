# Workflow: Discovery

## Purpose

Take a raw idea and produce a signed-off PRD committed to a new project repository.

## Input

A raw idea — unpolished is fine.

## Output

A `PRD.md` committed to a new project repository.

---

## Principles

- The PRD is tech-agnostic. Implementation details (frameworks, APIs, protocols) belong in a tech spec, not here.
- Do not write the PRD until open questions are resolved and the user has confirmed the framing.
- Do not create the project or commit anything until the user explicitly approves the final PRD.
- Name the user roles explicitly. If the product has two sides, define both from the start.
- Pressure-test the mechanism, not just the idea. Ask why it works this way.
- Ask focused questions in batches — not one at a time forever.
- Competitive discovery is not optional. It informs positioning, scope, and what belongs in Non-Goals.

---

## Steps

### 1 — Get the Raw Idea

Ask the user to share their idea. Unpolished is fine — do not ask for a structured brief.

---

### 2 — Pressure-Test the Idea

Ask focused questions to stress the idea. Group related questions and ask them together. Cover:

**Users**
- Who specifically are the users? Push for concrete scenarios, not demographics.
- Are there two sides (owner/recipient, sender/viewer, etc.)? Name them explicitly.

**The problem**
- What do people do today instead? What's painful about it?
- Is this a real recurring pain or a hypothetical one?

**The mechanism**
- Why does the product work this way? What does the specific interaction model unlock?
- What's the simplest version of this that would still solve the problem?

**Scope**
- Which parts are core and which are nice-to-have?
- What should be explicitly out of scope for the first version?

Listen to the answers. Adjust follow-up questions based on what's still unclear. Do not ask about things the user has already answered.

---

### 3 — Competitive Discovery

Before confirming framing, research what already exists in this space. Cover:

**Existing solutions**
- What products already solve this problem, fully or partially?
- What do they cost? What's free, what's paid, what's behind a paywall?
- Which ones require accounts, setup, or technical knowledge?

**Direct vs. indirect competition**
- What are people actually using today as a workaround, even if it's imperfect?
- Which competitors are technically closest to the proposed product?

**Gaps**
- What does no existing solution do well?
- What do users complain about most in reviews and forums?
- Where is the market map genuinely unoccupied?

Summarise findings back to the user. Let them react — they may adjust scope, positioning, or the core mechanism based on what already exists.

Use competitive findings to sharpen the PRD:
- Goals should reflect real gaps, not features that already exist everywhere
- Non-Goals should explicitly park things that incumbents already do well
- Key Product Decisions should be informed by what competitors got wrong

---

### 4 — Synthesize and Confirm Framing

After competitive discovery, reflect back:
- The core problem in one sentence
- Who the users are and what each of them does
- What the product is, stated plainly
- How it is meaningfully different from what already exists

Ask the user if this framing is right. Only proceed when confirmed.

---

### 5 — Draft the PRD

Write a tech-agnostic PRD using this structure:

```
# [Product Name] — Product Requirements Document

## Overview
One short paragraph: what the product is and how it works at the highest level.

## Problem
What's broken today. Be specific — reference the actual behaviour people resort to.

## Users
Named roles (e.g. Owner / Controller, Sender / Recipient). One short paragraph per role
describing who they are and what they do in the product.

## Goals
Bulleted list of what a successful MVP achieves.

## Non-Goals (MVP)
Bulleted list of things explicitly out of scope. Include deferred features with a "— deferred" label.

## Core User Stories
Grouped by role. Each story starts with "I can..." or "I get...".
Include cross-role stories in a "Both" section.

## Key Product Decisions
Markdown table: Decision | Choice | Rationale

## MVP Scope
Bulleted list of what ships in v1.

## Open Questions
Numbered list of unresolved decisions that need answers before the PRD is final.
```

---

### 6 — Resolve Open Questions

Present the open questions to the user and work through each one. Update the PRD as decisions are made. Remove resolved questions from the Open Questions section — decisions belong in Key Product Decisions or MVP Scope.

Do not finalize the PRD until all open questions are resolved.

---

### 7 — Final Approval and Commit

Present the final PRD to the user. Ask for explicit approval.

Once approved:
1. Ask where the project directory should live if not already known.
2. Create the project directory.
3. Write the PRD as `PRD.md` in the project root.
4. Run `git init` and commit with message `Add PRD`.
