# Planning Rules

------------------------------------------------------------

## Purpose

Planning converts a chosen direction into safe execution.

------------------------------------------------------------

## Plan Format

A plan must include:

- goal
- affected files
- affected data
- environment
- step-by-step actions
- risks
- verification
- rollback
- approvals needed

------------------------------------------------------------

## Size Rule

If a task touches more than 3 files, split it into smaller tasks.

Each subtask should be independently understandable and reviewable.

------------------------------------------------------------

## Risk Rule

High-risk work requires explicit approval before execution.

High-risk includes:

- deleting files
- moving data
- database changes
- Docker volume operations
- n8n data changes
- secrets
- financial tooling
- auth changes
- Git push or force push

------------------------------------------------------------
