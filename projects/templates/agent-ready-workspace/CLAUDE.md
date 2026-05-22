@AGENTS.md

## Claude-specific

The canonical content for this workspace lives under `.opencode/` (OpenCode is the primary runtime). When using Claude Code, read these by explicit path:

- Agent definitions: `.opencode/agents/<slug>.md`
- Skills (SKILL.md format): `.opencode/skills/<slug>/SKILL.md`
- Slash commands: `.opencode/commands/<slug>.md`
- Rules: `.opencode/rules/<slug>.md`

Claude-specific runtime settings: `.claude/settings.json` (permission denies).

If you want Claude's agent / skill picker UI to list the workspace's agents and skills, mirror them via symlinks or copy — see `docs/how-to-add-agents-skills.md` → "How to make Claude Code see them too".

## First prompt

> Analyze this workspace. Do not edit files. Read AGENTS.md, README.md, docs/overview.md, docs/runbook.md, .opencode/rules/dispatch-policy.md, and .opencode/rules/workflow.md. Summarize structure, risks, and next steps.

Use `/analyze` for the same orientation pass.
