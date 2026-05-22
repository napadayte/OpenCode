# Gemini CLI Instructions

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

## Gemini-Specific Behavior

Use Gemini for:

- alternative analysis
- large-context review
- documentation review
- risk analysis
- brainstorm comparison
- second-opinion review

Do not push.

Do not commit unless explicitly requested.

Ask before destructive commands.

Protect secrets, data, backups, databases, Docker volumes, and n8n data.

------------------------------------------------------------

## Suggested First Prompt

    Analyze this workspace. Do not edit files. Read AGENTS.md, README.md, docs/overview.md, docs/runbook.md, docs/rules/dispatch-policy.md, and docs/rules/workflow.md. Summarize structure, risks, and next steps.

------------------------------------------------------------
