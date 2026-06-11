# Workflow: Competitor Analysis

## Purpose

Map the existing solution landscape for a given problem space, understand what's paid vs. free, and surface the gaps that inform product positioning.

## Input

A product idea, problem description, or PRD.

## Output

A `spec/product/COMPETITOR_ANALYSIS.md` committed to the project repository.

---

## Principles

- Be honest about what competitors do well, not just their weaknesses.
- Distinguish between direct competitors (same problem, same approach) and indirect ones (same problem, different workaround).
- Do not invent or assume features — only report what is verifiable.
- Go beyond the obvious names. Look for open-source projects, niche tools, and what people actually use as workarounds today.
- The closest competitor is often not the most famous one.
- Gaps should be real and specific, not generic ("no one does this perfectly").

---

## Steps

### 1 — Understand the Problem Space

Extract from the input:
- The core problem being solved
- The target user and their scenario
- The key interaction model

---

### 2 — Build the Market Map

Search broadly. Cover:

**Direct competitors** — products that solve the same problem in a similar way
**Indirect competitors** — what people actually use as a workaround today (video calls, voice guidance, manual steps, etc.)
**Open-source / niche tools** — GitHub projects, F-Droid apps, community tools that mainstream users don't know about
**Adjacent products** — solutions that partially overlap (e.g. parental control apps, MDM tools)

Aim for thoroughness over brevity here. It is better to include a minor player and note why they are not a threat than to miss them entirely.

---

### 3 — Deep Dive on the Closest Competitors

Identify the 2–3 competitors that are technically or conceptually closest to the product being built. For each, research in detail:

- **Exact flow**: what does the user have to do to get started? Step by step.
- **Account model**: what is required on each side? Is there any account-free path?
- **Technical implementation**: how does it actually work under the hood?
- **Pricing**: what is free, what is paywalled, what are the specific limits on the free tier?
- **Limitations**: what can it not do? Any Android version restrictions, platform constraints, or known issues?
- **User sentiment**: what do reviews, Reddit, and forums say? What do users complain about most?
- **Distribution**: how do users find and install it? Play Store, sideload, GitHub?

---

### 4 — Identify Gaps and Opportunities

Synthesise the analysis into three categories:

**Common weaknesses** — pain points that appear across multiple competitors
**Underserved segments** — user types or scenarios that existing solutions ignore or handle poorly
**Positioning opportunities** — where the product being built can differentiate in a way that is both real and defensible

Gaps should be grounded in evidence (user reviews, pricing walls, missing features) — not wishful thinking.

---

### 5 — Competitive Summary Table

Produce a summary table comparing the most relevant competitors on the dimensions that matter most for this specific product. Choose dimensions that highlight the product's differentiation — not generic dimensions that make every competitor look the same.

---

### 6 — Output and Commit

Write `spec/product/COMPETITOR_ANALYSIS.md` using this structure:

```
# Competitor Analysis — [Product Name]

## Problem Space

## Market Map

### Commercial tools (table: product, platforms, account required, free tier, pricing)
### Open-source / no-account tools (table: product, how it connects, platform, constraints)
### Indirect competitors (what people actually do today)

## Deep Dives

### [Closest Competitor 1]
### [Closest Competitor 2]
### ...

## Technical Landscape (optional)
How existing solutions solve the technical problem — APIs, protocols, architectures used.

## User Sentiment and Pain Points
What users complain about across the space.

## Gaps and Opportunities

### Common weaknesses
### Underserved segments
### Positioning opportunities

## Competitive Summary Table
```

Ask the user to confirm before writing to disk and committing.
