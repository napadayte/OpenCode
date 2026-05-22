# Claude Code Instructions

------------------------------------------------------------

## Shared Contract

Follow the shared workspace contract:

    AGENTS.md

Read these first:

    README.md
    docs/overview.md
    docs/runbook.md
    docs/rules/dispatch-policy.md
    docs/rules/workflow.md

Read task-specific rules from:

    docs/rules/

------------------------------------------------------------

## Claude-Specific Behavior

Classify first.

Do not edit files before understanding the task.

Use brainstorm mode for:

- unclear tasks
- strategic decisions
- architecture decisions
- automation design
- data/database design
- financial scanner design
- tool choice

Use devil/reviewer thinking for important decisions.

Do not push.

Do not commit unless explicitly requested.

Ask before destructive commands.

Protect secrets, data, backups, databases, Docker volumes, and n8n data.

------------------------------------------------------------

## Suggested First Prompt

    Analyze this workspace. Do not edit files. Read AGENTS.md, README.md, docs/overview.md, docs/runbook.md, docs/rules/dispatch-policy.md, and docs/rules/workflow.md. Summarize structure, risks, and next steps.

------------------------------------------------------------
