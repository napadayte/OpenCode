# AGENTS.md

------------------------------------------------------------

## Role

This is an agent-ready workspace.

It is not primarily a coding project.

Agents must optimize for:

- clarity
- safety
- recoverability
- low chaos
- manual control
- long-term maintainability

Small code is allowed only when it supports the workspace.

------------------------------------------------------------

## First Action

For every non-trivial request:

1. Classify the task.
2. Identify the environment.
3. Identify affected files, data, tools, or services.
4. Ask clarification if the target is unclear.
5. Read the relevant rule files.
6. Plan before changing files.

Do not rush into edits.

------------------------------------------------------------

## Always Read First

Read these first:

    README.md
    docs/overview.md
    docs/runbook.md
    docs/rules/dispatch-policy.md
    docs/rules/workflow.md

------------------------------------------------------------

## Read When Relevant

For brainstorm or strategy:

    docs/rules/brainstorm.md

For planning:

    docs/rules/planning.md

For writing documentation:

    docs/rules/document-style.md

For git:

    docs/rules/git-operations.md

For data, databases, exports, backups, or market data:

    docs/rules/data-operations.md

For n8n or automation:

    docs/rules/automation-operations.md

For scripts, scanners, or helper tools:

    docs/rules/light-code-policy.md

For secrets, credentials, APIs, auth, risky commands, or external services:

    docs/rules/security.md

------------------------------------------------------------

## Task Types

Classify tasks as one of:

- brainstorm
- research
- planning
- documentation
- workspace setup
- automation
- n8n workflow
- data/database
- backup/recovery
- git sync
- light code
- security review
- cleanup
- troubleshooting
- review

If the task is ambiguous, ask before acting.

------------------------------------------------------------

## Mandatory Planning Triggers

Plan before action when the task involves:

- more than 3 files
- data or databases
- backups or restore
- Docker volumes
- n8n data
- credentials or auth files
- financial data
- stock scanner logic
- GitHub sync
- Windows / WSL / Mac sync
- automation workflow changes
- agent rules
- project templates
- deleting or moving files
- installing tools
- changing global configs

------------------------------------------------------------

## Safety

Do not do these unless explicitly approved by the user:

- push
- commit
- force push
- delete files
- remove data
- edit secrets
- expose credentials
- change databases
- touch Docker volumes
- modify n8n data
- install global tools
- run destructive commands

------------------------------------------------------------

## Data Protection

Data/database tasks require:

- data location
- data sensitivity
- backup or rollback path
- restore notes when relevant
- data inventory update when relevant

Read:

    docs/rules/data-operations.md

------------------------------------------------------------

## Light Code

Small scripts are allowed when useful.

Before writing code, define:

- goal
- input
- output
- run command
- dependencies
- risk
- verification

Read:

    docs/rules/light-code-policy.md

------------------------------------------------------------

## Final Report

After any change, report:

- changed files
- what changed
- why it changed
- how to verify
- remaining risks
- next recommended step

------------------------------------------------------------
