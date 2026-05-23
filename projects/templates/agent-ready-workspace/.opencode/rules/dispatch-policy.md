# Dispatch Policy

------------------------------------------------------------

## Purpose

Every non-trivial request must be classified before action.

The agent must not rush into edits.

------------------------------------------------------------

## First Action

For every task:

1. Classify the request.
2. Identify the environment.
3. Identify affected files, data, or tools.
4. Decide whether clarification is needed.
5. Decide whether brainstorm is needed.
6. Decide whether planning is needed.
7. Read relevant rule files.
8. Proceed only within scope.

------------------------------------------------------------

## Task Types

Classify as one of:

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

------------------------------------------------------------

## Clarification Required

Ask before acting when:

- target folder is unclear
- environment is unclear
- Windows, WSL, Docker, Conda, Mac, or cloud boundaries are unclear
- task may affect secrets
- task may affect data or databases
- task may delete or overwrite files
- task may touch more than 3 files
- expected output format is unclear
- user intent is strategic rather than operational

------------------------------------------------------------

## Dispatcher Rule

The dispatcher (`manager` agent) classifies, routes, and synthesizes.

The dispatcher must not perform specialist work or risky file edits directly. It delegates via the `task` tool and reports the routing decision to the user.

Every primary interaction starts with `manager`. Specialists (`planner`, `reviewer`, `data-operator`, etc.) are invoked by `manager`, not picked directly by the user.

------------------------------------------------------------
