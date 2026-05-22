# Runbook

------------------------------------------------------------

## Purpose

This file contains operational procedures for the workspace.

Use it for repeatable steps, recovery notes, and daily commands.

------------------------------------------------------------

## Daily Start

Check current state:

    pwd
    git status
    tree -a -L 3 -I '.git|node_modules|.cache' .

------------------------------------------------------------

## Before Changes

Before any non-trivial change:

1. Classify the task.
2. Read relevant rule files.
3. Check git status.
4. Create a plan.
5. Confirm risky actions.

------------------------------------------------------------

## After Changes

After changes:

    git status
    git diff

Then document:

- changed files
- what changed
- why changed
- verification
- risks
- next step

------------------------------------------------------------

## Recovery Notes

Document restore procedures here.

Examples:

- WSL restore
- Docker volume restore
- n8n restore
- database restore
- Git rollback

------------------------------------------------------------
