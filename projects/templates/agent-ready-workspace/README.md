# Workspace Name

------------------------------------------------------------

## Purpose

This is an agent-ready workspace.

It is designed for:

- documentation
- planning
- research
- brainstorms
- automation notes
- n8n workflows
- data and database inventory
- backup and recovery notes
- prompts
- checklists
- reports
- small helper scripts
- lightweight scanners and tools

This is not primarily a coding project.

Small code is allowed when it supports the workspace.

------------------------------------------------------------

## Current Status

Status:

    Draft

Fill this section with:

- what this workspace is for
- what is active now
- what is blocked
- what needs review

------------------------------------------------------------

## Main Documents

Start here:

    AGENTS.md
    docs/overview.md
    docs/runbook.md
    docs/rules/dispatch-policy.md
    docs/rules/workflow.md

Important rule files:

    docs/rules/brainstorm.md
    docs/rules/planning.md
    docs/rules/document-style.md
    docs/rules/git-operations.md
    docs/rules/data-operations.md
    docs/rules/automation-operations.md
    docs/rules/light-code-policy.md
    docs/rules/security.md

------------------------------------------------------------

## Main Folders

    docs/           Operating documentation and rules
    research/       Research notes and source summaries
    notes/          Informal notes
    prompts/        Reusable prompts
    checklists/     Repeatable checklists
    automations/    Automation and n8n documentation
    data/           Data inventory, schemas, local exports, backups
    tools/          Small scripts, scanners, helper tools

------------------------------------------------------------

## Safe First Prompt

Use this with any agent shell:

    Analyze this workspace. Do not edit files. Read AGENTS.md, README.md, docs/overview.md, docs/runbook.md, and docs/rules/workflow.md. Summarize the structure, risks, and next steps.

------------------------------------------------------------

## Daily Workflow

Before changes:

    git status

For non-trivial work:

1. Classify the task.
2. Brainstorm if needed.
3. Plan before changes.
4. Make small changes.
5. Review.
6. Check git status and diff.
7. Commit manually only when ready.

------------------------------------------------------------

## Never Commit

Never commit:

- secrets
- credentials
- tokens
- API keys
- auth files
- local database files
- database dumps
- exports with private data
- backup archives
- Docker volume backups
- n8n data backups
- broker credentials

------------------------------------------------------------
