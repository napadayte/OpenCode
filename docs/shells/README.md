# Agent Shells

------------------------------------------------------------

## Purpose

This folder documents the AI coding shells used in the WSL development environment.

------------------------------------------------------------

## Shell map

    OpenCode    -> main orchestrator and project workflow
    Codex CLI   -> OpenAI / ChatGPT subscription agent
    Claude Code -> Anthropic / Claude subscription agent
    Gemini CLI  -> Google / Gemini subscription agent

------------------------------------------------------------

## Main workspace

Projects live here:

    /home/bohdan/code

OpenCode config lives here:

    /home/bohdan/.config/opencode

OpenCode config repo:

    git@github.com:napadayte/OpenCode.git

------------------------------------------------------------

## Shared project contract

Every agent-ready project should have:

    AGENTS.md
    README.md
    docs/architecture.md
    docs/runbook.md

Optional tool adapters:

    CLAUDE.md
    GEMINI.md
    .opencode/instructions.md
    .codex/config.toml
    .claude/settings.json
    .gemini/settings.json

------------------------------------------------------------

## Never commit secrets

Never commit:

    .env
    .env.*
    auth.json
    tokens
    credentials
    API keys
    private keys
    ~/.codex/auth.json
    ~/.claude.json
    ~/.claude/
    ~/.gemini/oauth_creds.json
    ~/.gemini/google_accounts.json

------------------------------------------------------------
