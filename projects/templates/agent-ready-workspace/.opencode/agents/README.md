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

Each agent file is the single source of truth for OpenCode. YAML frontmatter follows the OpenCode agent schema:

```yaml
---
description: One sentence + trigger words (EN/RU/UA). Front-load keywords the user is likely to type.
mode: primary       # or "subagent" — primary appears in /agent picker, subagent is invoked via task tool
color: blue         # cosmetic
permission:
  edit: ask         # ask | allow | deny — coarse rule
  bash:             # per-pattern bash rules; default falls back to top-level opencode.json
    "*": ask
    "git status*": allow
    "git push*": deny
---
```

The file body becomes the agent's system prompt.

Rules:
- `name:` is NOT in frontmatter — OpenCode derives it from the filename.
- `model:` is intentionally omitted — workspace template stays model-agnostic; the user's `default_agent` / runtime model is used.
- `tools:` is NOT used — selection is via `permission` (the array form is Claude Code's, not OpenCode's).

## Mirroring to other shells

For Claude Code's `/agent` picker, copy or symlink each file into `.claude/agents/` and replace the frontmatter with Claude Code's shape (`name`, `description`, `model: sonnet|opus|haiku`, `tools: ["Read", "Write", ...]`). See `docs/how-to-add-agents-skills.md`.

## Adding an agent

1. Create `<slug>.md` (use `new-agent-doc <slug>` if the helper is installed).
2. Fill frontmatter with `description`, `mode`, `permission`. Be deliberate with `permission` (principle of least privilege).
3. Update `AGENTS.md` and this README so the new role is discoverable.
4. No edit to `opencode.json` is needed — the file is auto-loaded.
