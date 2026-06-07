# Command: commit

Inspect the current changes, generate a commit message consistent with the repository's style, and commit once approved.

**MANDATORY** Do not commit until the user explicitly approves the message.
**MANDATORY** Focus on the *why*, not the *what* — the diff already shows what changed.

---

## Step 1 — Inspect the Changes

Run in parallel:
- `git status` to see staged and unstaged files
- `git diff HEAD` to see all current changes
- `git log --oneline -10` to understand the repo's commit message style

---

## Step 2 — Generate the Commit Message

Analyse the changes and draft a commit message:
- One subject line (imperative mood, under 70 characters)
- Optional body if the change is complex enough to warrant explanation of the reasoning

Do not add a body just to fill space. If the subject line is sufficient, leave it at that.

---

## Step 3 — Present and Confirm

Show the proposed commit message to the user. Ask for approval or edits.

---

## Step 4 — Commit

Once approved, stage any unstaged files the user wants included and run the commit.
