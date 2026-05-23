# How To Use This System

------------------------------------------------------------

## 1. Purpose

This repo stores the agent workspace system.

It contains:

- OpenCode global config
- agent-ready project template
- agent-ready workspace template
- scripts for creating new projects and workspaces
- documentation for OpenCode, Codex, Claude, and Gemini

Main repo path:

    ~/.config/opencode

GitHub repo:

    git@github.com:napadayte/OpenCode.git

------------------------------------------------------------

## 2. Main Commands

Create a coding project:

    new-agent-project <project-name>

Create a documentation / research / automation workspace:

    new-agent-workspace <workspace-name>

Example:

    cd ~/code
    new-agent-workspace stock-scanner-workspace

------------------------------------------------------------

## 3. Where Projects Live

All active work should live in:

    ~/code

Examples:

    ~/code/my-app
    ~/code/stock-scanner-workspace
    ~/code/personal-ops

Do not work directly inside:

    ~/.config/opencode

unless you are changing the global system itself.

------------------------------------------------------------

## 4. When To Use Each Template

Use this for coding projects:

    new-agent-project <name>

Use this for documentation, research, automation, data, backups, n8n, planning, prompts, and light tools:

    new-agent-workspace <name>

Most of my work should use:

    new-agent-workspace

------------------------------------------------------------

## 5. Daily Workflow

Start work:

    cd ~/code/<workspace>
    git status
    tree -a -L 3 -I '.git|node_modules|.cache' .

Then open an agent shell:

    opencode

or:

    codex

or:

    gemini

or:

    claude

Use this first prompt:

    Analyze this workspace. Do not edit files. Read AGENTS.md, README.md, docs/overview.md, docs/runbook.md, .opencode/rules/dispatch-policy.md, and .opencode/rules/workflow.md. Summarize the structure, safety rules, task workflow, and next steps. Do not modify, commit, or push anything.

------------------------------------------------------------

## 6. Safe Work Rule

Before changes:

    git status

After changes:

    git status
    git diff

Do not commit automatically.

Do not push automatically.

Commit only after review.

Push only after review.

------------------------------------------------------------

## 7. What Agents Must Understand

Agents must understand:

- this is not always a coding project
- documentation is important
- data is important
- backups are important
- secrets must never be exposed
- git status must be checked
- dangerous commands require approval
- large tasks must be planned first

------------------------------------------------------------

## 8. Important Files In Every Workspace

Every generated workspace has:

    AGENTS.md
    README.md
    CLAUDE.md
    GEMINI.md
    opencode.json
    .opencode/instructions.md
    .opencode/agents/
    .opencode/skills/
    .opencode/commands/
    .opencode/rules/
    .claude/settings.json
    .codex/config.toml
    .gemini/settings.json
    docs/overview.md
    docs/runbook.md
    data/inventory.md

Start with:

    README.md
    docs/overview.md
    data/inventory.md

------------------------------------------------------------

## 9. Data Rule

Do not commit:

- real databases
- database dumps
- backups
- private exports
- API keys
- tokens
- credentials
- auth files
- n8n data backups
- broker credentials

Data assets must be documented in:

    data/inventory.md

------------------------------------------------------------

## 10. Backup Rule

Backups are not enough.

For important data, also document:

- where the backup is
- how to verify it
- how to restore it
- what can go wrong

Backup docs should go in:

    docs/runbook.md

or a specific file under:

    docs/

------------------------------------------------------------

## 11. Updating The Global System

To change templates or global instructions:

    cd ~/.config/opencode
    git status

Make changes.

Then check:

    git status
    git diff

Commit:

    git add .
    git commit -m "Clear commit message"
    git push

Final check:

    git status

Expected:

    nothing to commit, working tree clean

------------------------------------------------------------

## 12. Sync To Another Machine

On another machine:

    mkdir -p ~/code
    cd ~/.config
    git clone git@github.com:napadayte/OpenCode.git opencode

Then run the installer (it symlinks every script in tools/bin/ into `~/.local/bin/` and marks them executable):

    ~/.config/opencode/tools/bin/install-opencode-tools

Make sure PATH contains:

    ~/.local/bin

Check:

    which new-agent-project
    which new-agent-workspace

------------------------------------------------------------

## 13. Current Status

The system is ready.

Verified shells:

- OpenCode
- Codex
- Gemini
- Claude Code

Verified command:

    new-agent-workspace <name>

Verified result:

- correct README title
- main branch
- 38 workspace files
- 10 rule files
- git clean after read-only shell tests

------------------------------------------------------------
