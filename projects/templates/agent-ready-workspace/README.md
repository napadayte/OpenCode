# Workspace Name

Agent-ready workspace. Document-first, operations-first, safety-first.

Suitable for: documentation, planning, research, brainstorms, n8n workflows, data and database inventory, backup/recovery notes, prompts, checklists, reports, small helper scripts, lightweight scanners.

Not primarily a coding project. Small code is allowed when it supports the workspace.

## Status

```
Draft
```

Fill with: what this workspace is for, what's active, what's blocked, what needs review.

## Main documents

Start here:

- `AGENTS.md` — shared contract loaded by every shell
- `docs/overview.md` — what this workspace is for
- `docs/runbook.md` — routine operations and recovery
- `.opencode/rules/dispatch-policy.md` — how tasks are classified
- `.opencode/rules/workflow.md` — workflow pipeline

Other rules in `.opencode/rules/`. Agents in `.opencode/agents/`. Skills in `.opencode/skills/`. Slash commands in `.opencode/commands/`.

## Folders

| Folder | What lives here |
|---|---|
| `docs/` | Overview, runbook, decisions (ADR), plans, reports |
| `.opencode/` | Agents, skills, rules, commands (canonical content) |
| `.claude/` | Only Claude Code runtime settings (`settings.json`) |
| `research/` | Research notes and source summaries |
| `notes/` | Informal notes |
| `prompts/` | Reusable prompts |
| `checklists/` | Repeatable checklists |
| `automations/` | Automation and n8n workflow documentation |
| `data/` | Data inventory, schemas, local exports, backups |
| `tools/` | Small scripts, scanners, helper tools |

## Safe first prompt

```
Analyze this workspace. Do not edit files. Read AGENTS.md, README.md, docs/overview.md, docs/runbook.md, .opencode/rules/dispatch-policy.md, and .opencode/rules/workflow.md. Summarize structure, risks, and next steps.
```

Or run `/analyze` for the same orientation.

## Daily workflow

```
git status        # before
opencode          # or claude / codex / gemini
  /analyze        # orient
  /plan <task>    # produce plan in docs/plans/
  /review         # read-only review of pending diff
git status        # after
git diff
# commit manually only after review
```

Implementation is manual — read the plan in `docs/plans/`, apply small reviewable changes, then `/review`. There is no auto-implement command.

For non-trivial work:

1. Classify the task.
2. Brainstorm if architecture / automation / scanner choice.
3. Plan before changes (`/plan`).
4. Make small changes.
5. Review (`/review`).
6. Check `git status` and `git diff`.
7. Commit manually only when ready.

## Never commit

- secrets, credentials, tokens, API keys
- auth files (`auth.json`, `*.key`, `*.pem`)
- local database files (`*.sqlite`, `*.db`)
- database dumps
- exports with private data
- backup archives
- Docker volume backups
- n8n data backups
- broker credentials
