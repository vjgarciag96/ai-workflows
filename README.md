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
| [commit](workflows/git/commit.md) | Generate a commit message consistent with the repo's style |
