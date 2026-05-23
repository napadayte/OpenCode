# OpenCode Workspace Instructions

Follow `AGENTS.md` — same rules and structure apply.

## Read first

- `AGENTS.md`
- `README.md`
- `docs/overview.md`
- `docs/runbook.md`
- `.opencode/rules/dispatch-policy.md`
- `.opencode/rules/workflow.md`

Task-specific rules in `.opencode/rules/`. Agent roles in `.opencode/agents/`. Reusable skills in `.opencode/skills/`. Slash commands in `.opencode/commands/`.

## Recommended flow

```
/analyze            read-only orientation
/plan <task>        produce a step-by-step plan with risks and rollback
/review             read-only review of pending diff
/intake <path>      review a captured external asset
/inventory <asset>  update data/inventory.md
```

Implementation is manual: read the plan in `docs/plans/`, apply small reviewable changes, then `/review`.

## Behavior

- Classify first.
- Plan before non-trivial changes.
- Use brainstorm before architecture, automation, data, financial scanner, or tool choices.
- Do not push.
- Do not commit unless explicitly requested.
- Ask before destructive commands.
- Protect data, databases, backups, secrets, auth files, Docker volumes, and n8n data.
