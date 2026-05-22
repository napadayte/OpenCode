# OpenCode Workspace Instructions

------------------------------------------------------------

## Shared Contract

Follow:

    AGENTS.md

Read first:

    README.md
    docs/overview.md
    docs/runbook.md
    docs/rules/dispatch-policy.md
    docs/rules/workflow.md

Use task-specific rules from:

    docs/rules/

------------------------------------------------------------

## Recommended OpenCode Flow

For analysis:

    /analyze

For planning:

    /plan <task>

For approved changes:

    /fix <task>

For review:

    /review

------------------------------------------------------------

## Behavior

Classify first.

Plan before non-trivial changes.

Use brainstorm before architecture, automation, data, financial scanner, or tool-choice decisions.

Do not push.

Do not commit unless explicitly requested.

Ask before destructive commands.

Protect data, databases, backups, secrets, auth files, Docker volumes, and n8n data.

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
