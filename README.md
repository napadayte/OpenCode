# OpenCode Workspace System

Reusable global configuration for AI coding shells (OpenCode, Codex CLI, Claude Code, Gemini CLI).

This repo provides one shared project contract (`AGENTS.md`) and two templates that turn any folder into an agent-ready project understood by all four shells.

## What's inside

- `opencode.json` — OpenCode permissions, agents, commands
- `AGENTS.md` — shared contract every agent reads first
- `tools/bin/` — generator scripts (`new-agent-workspace`, `new-agent-project`, …)
- `projects/templates/` — two templates:
  - `agent-ready-workspace` — for documentation, research, automation, data, n8n, light scripts
  - `agent-ready-project` — for code-first projects
- `docs/` — architecture, daily workflow, shell-specific references

## Install

```bash
# Clone anywhere; the canonical location is ~/.config/opencode
git clone git@github.com:napadayte/OpenCode.git ~/.config/opencode

# Symlink generator scripts into ~/.local/bin (also marks them executable)
~/.config/opencode/tools/bin/install-opencode-tools

# Make sure ~/.local/bin is on PATH
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
```

The scripts auto-detect the repo from their own path, so they work from any clone location.

## Daily use

```bash
# Create a documentation / automation / research workspace
new-agent-workspace stock-scanner-research
cd ~/code/stock-scanner-research
opencode    # or: claude / codex / gemini

# Create a code-first project
new-agent-project my-app
cd ~/code/my-app
opencode
```

First prompt in any shell:

```
Analyze this workspace. Do not edit files. Read AGENTS.md, README.md, and docs/. Summarize structure, risks, and next steps.
```

## Safety defaults

- Never commit secrets, auth files, tokens, API keys, database dumps, or backups.
- Agents must not push or commit unless explicitly asked.
- Destructive commands require approval.
- Before any change: `git status`. After: `git status && git diff`.

## More

- `docs/architecture.md` — repo layout and workflow
- `docs/how-to-use.md` — extended usage guide
- `docs/agent-shells.md` — shell-specific notes (OpenCode, Codex, Claude, Gemini)
- `docs/how-to-add-agents-skills.md` — adding agents, skills, and rules
