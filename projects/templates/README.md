# Project Templates

------------------------------------------------------------

## Agent-ready project template

Template path:

    projects/templates/agent-ready-project

Working copy path:

    ~/code/_templates/agent-ready-project

------------------------------------------------------------

## How to create a new project from template

Example:

    cd ~/code
    cp -a ~/.config/opencode/projects/templates/agent-ready-project my-new-project
    cd my-new-project
    git init
    git branch -M main

Then edit:

    README.md
    AGENTS.md
    docs/architecture.md
    docs/runbook.md

------------------------------------------------------------

## Required files

Every agent-ready project should have:

    AGENTS.md
    README.md
    docs/architecture.md
    docs/runbook.md
    .gitignore

Optional adapter files:

    CLAUDE.md
    GEMINI.md
    .opencode/instructions.md
    .codex/config.toml
    .claude/settings.json
    .gemini/settings.json

------------------------------------------------------------

## Rules

Do not store secrets in templates.

Do not store:

    .env
    API keys
    tokens
    credentials
    auth files

Keep templates generic and reusable.

------------------------------------------------------------
