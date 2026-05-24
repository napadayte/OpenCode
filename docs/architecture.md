# Architecture

## Purpose

Reusable global configuration for AI coding shells (OpenCode, Codex CLI, Claude Code, Gemini CLI). Provides one shared project contract and two templates so any folder can be opened by any shell with consistent rules.

## Structure

```
~/.config/opencode/
├── README.md                  Entry point
├── AGENTS.md                  Shared contract loaded by every shell
├── opencode.json              OpenCode config: top-level permissions, agents, commands
├── package.json               Declares @opencode-ai/plugin (runtime dependency for OpenCode)
├── .opencode/instructions.md  Repo-global rules (loaded via opencode.json)
├── agents/                    Global OpenCode agents (mode: subagent), available across projects
├── skills/                    Global OpenCode skills (each skill in its own folder with SKILL.md)
├── docs/
│   ├── architecture.md        This file
│   ├── agent-shells.md        Per-shell notes (full reference)
│   ├── workspace-template-spec.md   Full workspace template spec
│   ├── audits/                Historical audits and follow-ups
│   ├── shells/{claude,codex,gemini,opencode}/   Per-shell instruction files
│   └── wiki/                  Visual Russian wiki (Obsidian-friendly)
├── projects/templates/
│   ├── agent-ready-project/     For code-first projects (minimal — only AGENTS/CLAUDE/GEMINI/README + docs/)
│   └── agent-ready-workspace/   For docs / research / automation / data (full .opencode/ with manager orchestrator)
└── tools/bin/
    ├── new-agent-workspace      Create a workspace from template
    ├── new-agent-project        Create a coding project from template
    ├── new-agent-doc            Add an agent doc inside a workspace
    ├── new-skill-doc            Add a skill doc inside a workspace
    ├── capture-agent-asset      Intake external rule/skill source safely
    └── install-opencode-tools   Symlink scripts into ~/.local/bin
```

`package.json` exists only to pin `@opencode-ai/plugin` so the plugin system resolves consistently across machines; `package-lock.json` is committed for reproducibility. Do not add other npm dependencies here — this is a config repo, not a Node project.

## Workflow

### Creating a new workspace

```
new-agent-workspace <name>     creates ~/code/<name> from agent-ready-workspace template
new-agent-project <name>       creates ~/code/<name> from agent-ready-project template
```

Each script:
1. Resolves the repo root from its own location (no hardcoded path).
2. Copies the template excluding `.git`, `node_modules`, caches, archives, auth files.
3. Replaces the README title and runs `git init` on the new folder.
4. Prints next steps.

### Per-session flow inside a workspace

```
opencode (or claude / codex / gemini)
  /analyze     →   read structure, summarize
  /plan        →   propose step-by-step plan, no edits
  /review      →   read-only review of current diff
  /intake      →   review a captured external asset
  /inventory   →   update data/inventory.md
```

Manual `git status` / `git diff` before and after every change. Commits and pushes are manual; agents never push.

### Adding agents or skills

Inside a workspace:
```
new-agent-doc <slug>      creates .opencode/agents/<slug>.md from a skeleton
new-skill-doc <slug>      creates .opencode/skills/<slug>/SKILL.md from a skeleton
```

External rules and prompts go through quarantined intake:
```
capture-agent-asset <file>      copies to research/agent-assets/<date>_<slug>/, writes review.md
```

See `docs/wiki/концепции/агент.md` and `docs/wiki/концепции/скилл.md` for agent/skill specs.

## Sync

The repo is synced via Git. The canonical clone location is `~/.config/opencode`; scripts work from any location. Per-machine secrets and local data live outside the repo (see `.gitignore`).

## Risks

- Do not commit secrets, API keys, auth files, tokens, database dumps, or local backups.
- Templates must stay generic — no machine-specific paths, no credentials.
- New agents and skills must be added through `new-agent-doc` / `new-skill-doc` or vetted intake — not by pasting external content directly.
- The two templates share documentation files; changes to one often require changes to the other.
