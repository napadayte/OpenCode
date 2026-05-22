# Gemini CLI Instructions

Follow `AGENTS.md` — same rules and structure apply.

Read first:

- `AGENTS.md`
- `README.md`
- `docs/overview.md`
- `docs/runbook.md`
- `.opencode/rules/dispatch-policy.md`
- `.opencode/rules/workflow.md`

Task-specific rules in `.opencode/rules/`. Agent roles in `.opencode/agents/`. Reusable skills in `.opencode/skills/`.

## Use Gemini for

- alternative analysis
- large-context review
- documentation review
- second-opinion brainstorm

## Rules

- Do not push.
- Do not commit unless explicitly requested.
- Ask before destructive commands.
- Protect secrets, data, backups, databases, Docker volumes, and n8n data.

## Suggested first prompt

> Analyze this workspace. Do not edit files. Read AGENTS.md, README.md, docs/overview.md, docs/runbook.md, .opencode/rules/dispatch-policy.md, and .opencode/rules/workflow.md. Summarize structure, risks, and next steps.
