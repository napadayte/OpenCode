@AGENTS.md

# OpenCode-specific addendum

The shared contract is in `AGENTS.md` (loaded above). This file only contains rules that are OpenCode-runtime-specific or workflow-specific to this repo — anything universal across shells belongs in `AGENTS.md` instead.

## Environment

- Prefer WSL as the main OpenCode environment.
- Keep generated projects under `~/code/` (one folder per project or workspace).
- Keep this global OpenCode config at `~/.config/opencode/` (XDG default — the clone of this repo). The generator scripts in `tools/bin/` resolve the repo root from their own location, but the wiki and several docs assume this canonical path.

## Wiki sync rule

- After adding or changing a provider, MCP server, agent, or skill in this repo — check `docs/wiki/обслуживание.md` and update the relevant wiki page before committing.
- If you notice something in the config that is not documented in the wiki, flag it as a gap and suggest running the `sync-wiki` skill.
- The `sync-wiki` skill lives at `skills/sync-wiki/SKILL.md` (global location per opencode.ai/docs — `~/.config/opencode/skills/<name>/SKILL.md`). Use it for a full audit.
