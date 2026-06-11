# ai-workflows

A personal, opinionated collection of AI workflows covering the full engineering lifecycle — from product discovery to implementation and deployment.

Workflows are extracted from real project work, not designed in the abstract. They are AI-provider-agnostic by design.

---

## Structure

```
workflows/          # Canonical workflow definitions (provider-agnostic)
providers/
  claude-code/      # Adapters for Claude Code slash commands
```

Each workflow lives in `workflows/` as the single source of truth. Provider-specific adapters in `providers/` are self-contained copies formatted for that provider's conventions. When a canonical workflow changes, its adapters should be updated to match.

---

## Installation

### Claude Code

Copy the commands you want to your global Claude Code commands directory:

```bash
cp providers/claude-code/*.md ~/.claude/commands/
```

They will be available as slash commands in any project (e.g. `/discovery`).

---

## Workflows

| Workflow | Description |
|---|---|
| [discovery](workflows/product/discovery.md) | Take a raw idea and produce a signed-off PRD |
| [competitor-analysis](workflows/product/competitor-analysis.md) | Map the solution landscape and surface positioning gaps |
| [prd-review](workflows/product/prd-review.md) | Run a structured multi-perspective review of a PRD using the full team |
| [product-design](workflows/design/product-design.md) | Take a signed-off PRD and produce an interactive HTML prototype covering all screens and states |
| [product-design-review](workflows/design/product-design-review.md) | Run a structured multi-perspective review of a product design document; surface missing states, spec gaps, and developer ambiguities |
| [tech-spec](workflows/engineering/tech-spec.md) | Take a signed-off PRD and design doc and produce a complete technical specification; two-phase: pre-spec engineering review then full-team post-spec review |
| [commit](workflows/git/commit.md) | Generate a commit message consistent with the repo's style |

---

## Team

The review team is defined in [`workflows/team/`](workflows/team/). Each team member has their own file with their role, focus areas, and voice. They are used by the `prd-review` workflow and any other workflow that benefits from multi-perspective input.

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
| Victor | Senior Android Engineer (product owner) |
