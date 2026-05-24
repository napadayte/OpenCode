---
description: Read-only orientation pass — understand the current folder before editing
---

Analyze the current folder. Do not edit files.

Read in order:
1. `AGENTS.md` (or `README.md` if missing) for the project contract.
2. Top-level structure (folders, key entry-point files).
3. Any `docs/` you find — especially `architecture.md`, `runbook.md`, `overview.md`.
4. If `.opencode/`, `.claude/`, or shell-specific config exists, note what agents/skills/commands are wired up.

Then summarize:
- **Purpose** — what this project is for, in one sentence.
- **Stack** — languages, frameworks, key dependencies.
- **Structure** — important directories and their roles.
- **Entry points** — how the project is run, built, or used.
- **Risks** — anything that looks fragile, undocumented, or dangerous.
- **Next steps** — what a new contributor should read or do first.

Stop after the summary. Do not propose changes unless asked.
