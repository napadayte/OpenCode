---
name: git-safe-commit
description: "Commit changes safely: status check, staged-diff review, secret scan, message draft, then manual commit. NEVER auto-pushes. На русском: безопасный коммит, проверь diff, закоммитить вручную, секреты. Українською: безпечний коміт, перевір diff."
---

# Git Safe Commit Skill

A reusable procedure for committing workspace changes without leaking secrets or mixing scopes.

## When to use

- before any user-approved commit
- after operator finishes a planned step
- after docs-writer updates documentation

## Procedure

### 1. Inspect state

```bash
git status
git branch --show-current
```

If unexpected changes appear (untracked secrets, database files, backup archives, files outside the requested scope), **stop and report**.

### 2. Review staged changes

```bash
git diff --cached
git diff --cached --stat
```

Read every file in the diff. Confirm:
- changes match the approved plan
- no secrets, tokens, API keys, passwords, OAuth values
- no database dumps, exports, or backup archives
- no machine-specific paths

### 3. Secret scan

Grep the staged diff for:
- `password=`, `secret=`, `token=`, `Bearer `, `Authorization:`
- `*_API_KEY`, `AWS_*`, `OPENAI_*`, `ANTHROPIC_*`
- `BEGIN PRIVATE KEY`, `BEGIN RSA`
- `https://hooks.slack.com/`, `https://discord.com/api/webhooks/`
- common database URLs (`postgres://user:pass@`, `mysql://user:pass@`)

If any hit: stop, do not commit, ask user.

### 4. Group commits by purpose

If the diff spans multiple unrelated changes, split into separate commits.

### 5. Draft commit message

Format:
```
<imperative subject ≤ 70 chars>

<body: what changed, why, how to verify>
```

Subject conventions:
- `Add ...` — new feature / file
- `Update ...` — change to existing
- `Fix ...` — bug fix
- `Document ...` — docs only
- `Remove ...` — deletion

Avoid: `update`, `fix`, `stuff`, `work`, `changes`.

### 6. Commit only after explicit user approval

```bash
git commit -m "<subject>" -m "<body>"
```

### 7. Verify

```bash
git status        # expect: nothing to commit
git log -1 --stat # confirm the commit landed as expected
```

## Push policy

Pushing is **a separate skill**. Do not push automatically. The user must explicitly request push.

## Restrictions

- Never commit without showing the user the staged diff first.
- Never use `git add -A` or `git add .` if unstaged files include anything outside the planned scope — stage files explicitly.
- Never bypass hooks with `--no-verify`.
- Never amend commits that have been pushed.
- Never force-push without explicit confirmation.

## Output

- Commit hash
- Subject line
- Files in commit (with `git show --stat HEAD`)
- Verification: `git status` clean
