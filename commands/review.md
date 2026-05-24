---
description: Read-only review of the current pending diff
---

Review the current git diff. Do not edit files.

Run:
- `git status` — what is staged, unstaged, untracked.
- `git diff` — full diff of unstaged changes.
- `git diff --cached` — full diff of staged changes.

Then evaluate:
- **Correctness** — does the change do what it claims?
- **Bugs** — logic errors, off-by-one, null/empty cases, race conditions.
- **Security** — secrets, injection, unsafe deserialization, permission leaks.
- **Tests** — is changed behavior covered? Any test that should fail still passes?
- **Maintainability** — naming, structure, comments, dead code.
- **Scope creep** — unrelated edits mixed in?
- **Style consistency** — matches the surrounding code?

Report findings as a numbered list, severity-tagged (critical / important / nit). Do not suggest a fix unless asked. Do not commit, push, or modify files.
