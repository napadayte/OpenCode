# Claude Code

------------------------------------------------------------

## Purpose

Claude Code is used as the Anthropic / Claude subscription-based coding agent.

It is separate from OpenCode and Codex.

------------------------------------------------------------

## Local install

Check:

    which claude
    claude --version
    claude doctor

------------------------------------------------------------

## Auth

Claude Code should be authenticated through Claude account login when using a Claude subscription.

Do not commit Claude auth files.

Never commit:

    ~/.claude.json
    ~/.claude/
    auth files
    tokens
    API keys
    credentials
    local session files
    logs
    cache files

------------------------------------------------------------

## Safe project files

Safe files that may exist inside project repos:

    CLAUDE.md
    .claude/settings.json

These files must not contain secrets.

------------------------------------------------------------

## Recommended first prompt

Run inside a project:

    cd ~/code/my-project
    claude

Prompt:

    Analyze this project. Do not edit files. Read AGENTS.md, README.md, docs/architecture.md, CLAUDE.md, GEMINI.md and summarize the structure.

------------------------------------------------------------

## Rules

- Follow AGENTS.md.
- Read docs/architecture.md before architecture changes.
- Do not push.
- Do not commit unless explicitly requested.
- Ask before destructive commands.
- Do not edit secrets.
- Prefer small, reviewable changes.
- Summarize changed files and verification.

------------------------------------------------------------
