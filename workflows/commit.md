# Workflow: Commit

## Purpose

Inspect the current changes, generate a commit message consistent with the repository's style, and commit once approved.

## Input

The current repository state (staged and unstaged changes).

## Output

A git commit with a well-formed message.

---

## Principles

- Focus on the *why*, not the *what*. The diff already shows what changed.
- Match the style and tone of recent commits in the repo.
- Keep the subject line short (under 70 characters).
- Do not commit unless the user explicitly approves the message.
- Do not include co-authors, tickets, or metadata unless the repo's history shows that pattern.

---

## Steps

### 1 — Inspect the Changes

Run in parallel:
- `git status` to see staged and unstaged files
- `git diff HEAD` to see all current changes
- `git log --oneline -10` to understand the repo's commit message style

---

### 2 — Generate the Commit Message

Analyse the changes and draft a commit message:
- One subject line (imperative mood, under 70 characters)
- Optional body if the change is complex enough to warrant explanation of the reasoning

Do not add a body just to fill space. If the subject line is sufficient, leave it at that.

---

### 3 — Present and Confirm

Show the proposed commit message to the user. Ask for approval or edits.

---

### 4 — Commit

Once approved, stage any unstaged files the user wants included and run the commit.
