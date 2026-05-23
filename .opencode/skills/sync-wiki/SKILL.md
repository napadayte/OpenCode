---
name: sync-wiki
description: Check whether the global OpenCode config is fully documented in the wiki. Reads providers, MCP servers, agents, and skills from the config — then checks each against the wiki. Reports gaps. Read-only, no edits.
---

# Sync-Wiki Skill

A read-only audit that compares what is actually configured globally with what is documented in the wiki. Reports gaps — does not edit.

## When to use

- After adding a new provider, MCP server, agent, or skill to `~/.config/opencode/`
- Periodically (monthly check from `обслуживание.md`)
- When wiki and config may have drifted after several changes

## Steps

### 1. Read the global config

Read `~/.config/opencode/opencode.json`. Extract:
- `provider` block — list all configured providers and their model names
- `mcp` block — list all configured MCP servers

### 2. Read the global agent and skill lists

List files in:
- `~/.config/opencode/.opencode/agents/` (if exists)
- `~/.config/opencode/.opencode/skills/` (if exists)

### 3. Read the wiki

Read these wiki pages:
- `~/.config/opencode/docs/wiki/провайдеры.md` — should list all providers and MCP servers
- `~/.config/opencode/docs/wiki/обслуживание.md` — maintenance checklists

### 4. Compare and report

For each item found in config or filesystem, check if it appears in the wiki.

Report in this format:

```
## Sync-Wiki Report

### Documented ✅
- <item> — found in wiki/<page>

### Missing from wiki ⚠️
- <item> — in opencode.json but not in провайдеры.md
- <item> — agent file exists but not listed in wiki

### Wiki entries with no config match ℹ️
- <item> — documented but not found in current config (may be intentional)

### Recommended actions
- [ ] Add <item> to wiki/провайдеры.md
- [ ] Remove stale entry <item> from wiki
```

## Restrictions

- Do not edit any file.
- Do not commit or push.
- Report only — let the user decide what to update.
- If `~/.config/opencode/` path is not accessible, say so and stop.
