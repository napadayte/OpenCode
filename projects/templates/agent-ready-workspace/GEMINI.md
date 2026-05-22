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


------------------------------------------------------------

## Agents And Skills

This workspace has explicit agent roles and repeatable skills.

Agents live in:

    agents/

Skills live in:

    skills/

Rules live in:

    docs/rules/

Use this meaning:

    agent = who performs the task
    skill = how to perform the task
    rule  = required constraint or safety boundary

Before non-trivial work:

1. classify the task
2. choose relevant agent role
3. choose relevant skill
4. read relevant rules
5. plan before changing files

Common agent roles:

- agents/brainstormer.md
- agents/planner.md
- agents/devil.md
- agents/reviewer.md
- agents/security-reviewer.md
- agents/data-operator.md
- agents/automation-operator.md
- agents/git-operator.md
- agents/docs-writer.md
- agents/light-code-helper.md

Common skills:

- skills/brainstorm.md
- skills/planning.md
- skills/security-check.md
- skills/git-safe-commit.md
- skills/data-inventory.md
- skills/backup-restore.md
- skills/n8n-workflow-doc.md
- skills/document-writing.md
- skills/light-code-script.md
- skills/stock-scanner-research.md

------------------------------------------------------------
