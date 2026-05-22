# Codex CLI

------------------------------------------------------------

## Purpose

Codex CLI is used as the OpenAI / ChatGPT subscription-based coding agent.

It is separate from OpenCode.

------------------------------------------------------------

## Local install

Binary example:

    ~/.nvm/versions/node/<version>/bin/codex

Check:

    which codex
    codex --version

------------------------------------------------------------

## Auth

Codex is authenticated through ChatGPT account login.

Do not commit Codex auth files.

Never commit:

    ~/.codex/auth.json
    ~/.codex/history.jsonl
    ~/.codex/*.sqlite
    ~/.codex/*.sqlite-shm
    ~/.codex/*.sqlite-wal
    ~/.codex/cache/
    ~/.codex/log/
    ~/.codex/.tmp/

------------------------------------------------------------

## Safe files

Safe reference file:

    docs/shells/codex/AGENTS.md

This is a copy of the global Codex instructions without secrets.

------------------------------------------------------------

## Project usage

Run inside a project:

    cd ~/code/my-project
    codex

Recommended first prompt:

    Analyze this project. Read AGENTS.md, README.md, and docs/architecture.md. Do not edit files.

------------------------------------------------------------

## Rules

- Do not push.
- Do not commit unless explicitly requested.
- Ask before destructive commands.
- Do not edit secrets.
- Prefer small, reviewable changes.
- Summarize changed files and verification.

------------------------------------------------------------
