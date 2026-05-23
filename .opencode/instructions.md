# OpenCode Global Instructions

This is the global OpenCode configuration workspace.

Rules:

- Prefer WSL as the main OpenCode environment.
- Keep projects under `~/code/` (one folder per project or workspace).
- Keep this global OpenCode config at `~/.config/opencode/` (XDG default — the clone of this repo).
- Do not store secrets, API keys, auth files, tokens, or local credentials in this repo.
- Do not push automatically.
- Do not commit unless explicitly requested.
- Ask before destructive commands.
- Make small, reviewable changes.
- Always summarize changed files and verification steps.

Wiki sync rule:

- After adding or changing a provider, MCP server, agent, or skill in this repo — check `docs/wiki/обслуживание.md` and update the relevant wiki page before committing.
- If you notice something in the config that is not documented in the wiki, flag it as a gap and suggest running the `sync-wiki` skill.
- The `sync-wiki` skill lives at `.opencode/skills/sync-wiki/SKILL.md` — use it for a full audit.
