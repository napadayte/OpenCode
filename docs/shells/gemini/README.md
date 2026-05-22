# Gemini CLI

------------------------------------------------------------

## Purpose

Gemini CLI is used as the Google / Gemini subscription-based coding agent.

It is separate from OpenCode, Codex, and Claude Code.

------------------------------------------------------------

## Local install

Check:

    which gemini
    gemini --version

------------------------------------------------------------

## Auth

Gemini CLI should be authenticated through Google login when using a Google subscription.

Do not commit Gemini auth files.

Never commit:

    ~/.gemini/oauth_creds.json
    ~/.gemini/google_accounts.json
    ~/.gemini/trustedFolders.json
    ~/.gemini/state.json
    ~/.gemini/history/
    ~/.gemini/tmp/
    ~/.gemini/cache/
    auth files
    tokens
    API keys
    credentials

------------------------------------------------------------

## Safe project files

Safe files that may exist inside project repos:

    GEMINI.md
    .gemini/settings.json

These files must not contain secrets.

------------------------------------------------------------

## Recommended first prompt

Run inside a project:

    cd ~/code/my-project
    gemini

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
