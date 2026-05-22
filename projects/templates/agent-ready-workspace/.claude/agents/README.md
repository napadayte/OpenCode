# Agents

Roles available in this workspace. See each `<slug>.md` for the full definition.

| Agent | Role | Edits? |
|---|---|---|
| [planner](planner.md) | Step-by-step plan with risks, verification, rollback | plan files only |
| [brainstormer](brainstormer.md) | Option generation before design | no |
| [devil](devil.md) | Read-only critic of plans and decisions | no |
| [reviewer](reviewer.md) | Read-only review of pending work | no |
| [security-reviewer](security-reviewer.md) | Secret / risk audit | no |
| [data-operator](data-operator.md) | Data, databases, exports, backups | yes |
| [automation-operator](automation-operator.md) | n8n and automation design + docs | docs only |
| [git-operator](git-operator.md) | Git ops (manual commit / push, never force) | no edits, runs git |
| [docs-writer](docs-writer.md) | Workspace documentation | docs only |
| [light-code-helper](light-code-helper.md) | Small Python / Bash scripts | code only |

## Format

Each agent file starts with YAML frontmatter:

```yaml
---
name: <slug>
description: "<one sentence + trigger words (EN, RU, UA)>"
model: <opus | sonnet | haiku>
color: <color>
tools:
  - <Tool>
---
```

Then the body describes purpose, when to use, restrictions, output format.

## Adding an agent

1. Run `new-agent-doc <slug>` from inside the workspace (skeleton creator).
2. Fill the YAML frontmatter — explicit `tools:` whitelist (principle of least privilege).
3. Update `AGENTS.md` and `.claude/agents/README.md` so the new role is discoverable.
4. If OpenCode should know it, add an entry under `agent` in `opencode.json`.
