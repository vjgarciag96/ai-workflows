# Command: competitor-analysis

Map the existing solution landscape for a given problem space, understand what's paid vs. free, and surface the gaps that inform product positioning.

**MANDATORY** Only report verifiable information. Do not invent or assume competitor features.
**MANDATORY** Be honest about what competitors do well, not just their weaknesses.
**MANDATORY** Go beyond the obvious names — look for open-source projects, niche tools, and what people actually use as workarounds.
**MANDATORY** Do not write the file until the user confirms the findings.

---

## Step 1 — Understand the Problem Space

Read the input (PRD, product description, or problem statement) and extract:
- The core problem being solved
- The target user and their scenario
- The key interaction model

If no input is provided, ask the user for a brief description before proceeding.

---

## Step 2 — Build the Market Map

Search broadly. Cover:

**Direct competitors** — products that solve the same problem in a similar way
**Indirect competitors** — what people actually use as a workaround today
**Open-source / niche tools** — GitHub projects, F-Droid apps, community tools mainstream users don't know about
**Adjacent products** — solutions that partially overlap

Aim for thoroughness. It is better to include a minor player than to miss one.

---

## Step 3 — Deep Dive on the Closest Competitors

Identify the 2–3 competitors that are technically or conceptually closest to the product. For each, research in detail:

- **Exact flow**: what does the user have to do to get started, step by step?
- **Account model**: what is required on each side? Any account-free path?
- **Technical implementation**: how does it actually work?
- **Pricing**: what is free, what is paywalled, what are the specific free tier limits?
- **Limitations**: what can it not do? Platform constraints, Android version restrictions, known issues?
- **User sentiment**: what do reviews, Reddit, and forums say? What do users complain about most?
- **Distribution**: Play Store, sideload, GitHub? How do mainstream users find it?

---

## Step 4 — Identify Gaps and Opportunities

Synthesise into three categories:

**Common weaknesses** — pain points appearing across multiple competitors
**Underserved segments** — user types or scenarios existing solutions ignore
**Positioning opportunities** — where the product can differentiate in a real and defensible way

Ground gaps in evidence (reviews, pricing walls, missing features) — not wishful thinking.

---

## Step 5 — Competitive Summary Table

Produce a summary table comparing the most relevant competitors on the dimensions that best highlight the product's differentiation.

---

## Step 6 — Present, Confirm, and Commit

Present the full analysis to the user. Ask for confirmation before writing to disk.

Once confirmed, write `spec/product/COMPETITOR_ANALYSIS.md` using this structure:

```
# Competitor Analysis — [Product Name]

## Problem Space

## Market Map
### Commercial tools
### Open-source / no-account tools
### Indirect competitors

## Deep Dives
### [Closest Competitor 1]
### [Closest Competitor 2]

## Technical Landscape (if relevant)

## User Sentiment and Pain Points

## Gaps and Opportunities
### Common weaknesses
### Underserved segments
### Positioning opportunities

## Competitive Summary Table
```

Then commit with message `Add competitor analysis`.
