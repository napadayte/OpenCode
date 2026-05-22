# Workflow Rules

------------------------------------------------------------

## Core Rules

- Classify first.
- Do not rush.
- Brainstorm before architecture.
- Plan before changes.
- Protect data.
- Protect secrets.
- Keep tasks small.
- Stop and re-plan on surprises.
- Review before commit.
- Commit manually.
- Push manually.
- Report every change.

------------------------------------------------------------

## Mandatory Pipeline Triggers

Use a pipeline when the task involves:

- more than 3 files
- data or databases
- backups
- restore operations
- Docker volumes
- n8n data
- credentials
- auth files
- financial data
- stock scanner logic
- GitHub sync
- Windows / WSL / Mac sync
- automation workflow changes
- agent rules
- project templates
- deleting files
- moving files
- installing tools
- changing global configs

------------------------------------------------------------

## Stop and Re-plan

Stop immediately when:

- command output is unexpected
- path is not expected
- git status shows unrelated changes
- conflict appears
- secret file appears
- data file appears unexpectedly
- command may delete data
- Windows and WSL paths are mixed
- Docker or volume operation is unclear
- backup is missing before risky operation
- agent is unsure

Do not continue through uncertainty.

------------------------------------------------------------

## Final Report

After work, report:

- changed files
- what changed
- why changed
- how to verify
- remaining risks
- next recommended step

------------------------------------------------------------
