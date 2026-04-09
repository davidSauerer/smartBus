---
description: Stage, commit with a professional message, and push all changes to the remote repository.
allowed-tools: Bash, Read, Glob
argument-hint: [optional commit message override]
---

You are responsible for cleanly committing and pushing all pending changes in this repository.

Follow these steps precisely:

## 1. Assess the current state

Run these in parallel:
- `git status` — identify all staged, unstaged, and untracked files
- `git diff HEAD` — understand what has changed in tracked files
- `git log --oneline -5` — see recent commit style for this repo

## 2. Identify what to stage

Stage all relevant changes. Exclude:
- Files that likely contain secrets (`.env`, credentials, tokens)
- Build artefacts or generated files that belong in `.gitignore`

Use specific file paths rather than `git add .` where possible. If untracked files look intentional (new ADRs, new skill files, config), include them.

## 3. Write a professional commit message

If `$ARGUMENTS` contains a message, use it as-is.

Otherwise, derive a commit message from the diff:
- **Subject line** (≤72 chars): imperative mood, no period — e.g. `Add vehicle selection ADR with initial requirements`
- **Body** (optional, if changes are non-trivial): bullet points summarising *what* changed and *why*, wrapped at 72 chars
- Follow the existing commit style found in `git log`

Format:
```
<subject line>

<body — only if needed>

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>
```

## 4. Commit and push

```bash
git add <files>
git commit -m "..."
git push
```

If the push fails because the remote branch does not exist yet, run:
```bash
git push --set-upstream origin <current-branch>
```

Report the final status: what was committed, the commit hash, and whether the push succeeded.
