---
description: Read-only review of pending changes
agent: reviewer
subtask: true
---

Use the `reviewer` and `security-reviewer` agents from `.opencode/agents/`.

Procedure:

1. Run `git status` and `git diff` (or `git diff --cached` if changes are staged).
2. Read `.opencode/rules/git-operations.md`, `.opencode/rules/security.md`.
3. Use the `security-check` skill from `.opencode/skills/security-check/SKILL.md`.

Report findings — **do not edit anything**.

Output:

- **Summary** — one-sentence verdict
- **Critical** — must fix before commit
- **Important** — should fix before commit
- **Suggestions** — optional improvements
- **Security findings** — secrets, dangerous commands, exposed paths
- **Approval** — APPROVE / REQUEST CHANGES / BLOCK

For each finding: file path, line, what's wrong, suggested action.

Do not commit. Do not push. Do not run destructive commands.
