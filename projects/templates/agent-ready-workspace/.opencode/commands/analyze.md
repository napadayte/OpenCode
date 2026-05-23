---
description: Analyze this workspace without editing files
agent: planner
---

Read these files in order — do not edit anything:

- `README.md`
- `AGENTS.md`
- `docs/overview.md`
- `docs/runbook.md`
- `.opencode/rules/dispatch-policy.md`
- `.opencode/rules/workflow.md`
- `data/inventory.md` (if present)

Summarize:

1. **Workspace purpose** — what this workspace is for, in one paragraph.
2. **Active workstreams** — what is currently in progress.
3. **Structure** — main folders and what lives in each.
4. **Risks** — what's most likely to break or leak.
5. **Next recommended step** — one concrete action.
6. **Global config gaps** — if `~/.config/opencode/opencode.json` is readable, check whether any providers or MCP servers configured there are missing from `~/.config/opencode/docs/wiki/провайдеры.md`. Report gaps as open questions. Skip silently if the path is not accessible.

Do not edit. Do not commit. Do not push. Do not run destructive commands.

If something is missing or unclear, surface it as an open question — do not guess.
