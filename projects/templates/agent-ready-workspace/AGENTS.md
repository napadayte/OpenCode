@.opencode/rules/dispatch-policy.md
@.opencode/rules/workflow.md
@.opencode/rules/git-operations.md
@.opencode/rules/security.md

# AGENTS.md

This is an agent-ready workspace. It is **not** primarily a coding project.

Optimize for: clarity, safety, recoverability, low chaos, manual control, long-term maintainability.

## Meaning

```
agent   = who performs the task   → .opencode/agents/
skill   = how to perform the task → .opencode/skills/<name>/SKILL.md
rule    = required constraint     → .opencode/rules/
command = reusable slash command  → .opencode/commands/
```

## Read on demand (task-specific rules)

| If the task involves | Read |
|---|---|
| Data, databases, exports, backups, restore | `.opencode/rules/data-operations.md` |
| n8n or automation workflows | `.opencode/rules/automation-operations.md` |
| Scripts, scanners, helper tools | `.opencode/rules/light-code-policy.md` |
| Documentation, README, runbook, ADR | `.opencode/rules/document-style.md` |
| Brainstorm or strategic decisions | `.opencode/rules/brainstorm.md` |
| Planning multi-step work | `.opencode/rules/planning.md` |

## Agents (`.opencode/agents/`)

| Agent | Role | Edits? |
|---|---|---|
| `planner` | Multi-step plan with risks, verification, rollback | plan files only |
| `brainstormer` | Option generation before design | no |
| `devil` | Read-only critic of plans and decisions | no |
| `reviewer` | Read-only review of pending work | no |
| `security-reviewer` | Secret / risk audit | no |
| `data-operator` | Data, databases, exports, backups | yes |
| `automation-operator` | n8n and automation design + docs | docs only |
| `git-operator` | Git ops (manual commit / push, never force) | no edits, runs git |
| `docs-writer` | Workspace documentation | docs only |
| `light-code-helper` | Small Python / Bash scripts | code only |

## Skills (`.opencode/skills/`)

| Skill | Purpose |
|---|---|
| `brainstorm` | Option-generation procedure with understanding lock |
| `planning` | Step-by-step plan with verification and rollback |
| `git-safe-commit` | Inspect → secret scan → manual commit |
| `data-inventory` | Maintain `data/inventory.md` |
| `backup-restore` | Backup + verified restore + runbook entry |
| `n8n-workflow-doc` | Document an n8n workflow safely |
| `security-check` | Read-only secret + risk audit |
| `document-writing` | Conventions per doc type |
| `light-code-script` | Small helper scripts (stdlib first) |
| `stock-scanner-research` | Research-only scanner (never trades) |

## Commands (`.opencode/commands/`)

- `/analyze` — read-only orientation pass
- `/plan <task>` — produce a plan file under `docs/plans/`
- `/review` — read-only review of pending diff
- `/intake <path>` — review a captured external asset
- `/inventory <asset>` — update `data/inventory.md`

## First action — always

1. Classify the task.
2. Identify the environment (WSL / Docker / Conda / GitHub / OneDrive / Mac / cloud).
3. Identify affected files, data, tools.
4. Ask one clarifying question if anything is unclear.
5. Read the rules listed above that match the task.
6. Plan before editing.

## Safety — non-negotiable

- Do not push.
- Do not commit unless explicitly requested.
- Do not run destructive commands without approval.
- Do not expose secrets, credentials, tokens, auth files.
- Do not modify data / Docker volumes / n8n storage without a documented backup + restore path.
- Stop and re-plan on surprise.

## Final report — always

After any change, report:
- changed files
- what changed
- why
- how to verify
- remaining risks
- next recommended step
