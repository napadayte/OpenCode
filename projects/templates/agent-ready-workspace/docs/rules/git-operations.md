# Git Operations Rules

------------------------------------------------------------

## Purpose

Git is used for synchronization, review, rollback, and portability.

Git must not be used casually for destructive operations.

------------------------------------------------------------

## Default Rule

Agents must not commit or push unless explicitly requested.

Manual user control is preferred.

------------------------------------------------------------

## Before Git Changes

Before staging, committing, pulling, merging, or pushing:

    git status
    git diff
    git log --oneline --max-count=5

Understand the current state first.

------------------------------------------------------------

## Commit Readiness

Commit only when:

- changes are intentional
- no secrets are staged
- no backups are staged
- no databases are staged
- no exports are staged
- generated files are excluded
- verification was done
- commit message is clear

------------------------------------------------------------

## Never Commit

Usually never commit:

- .env
- auth files
- credentials
- tokens
- caches
- node_modules
- backup archives
- raw exports
- database files
- large generated files
- personal local state

------------------------------------------------------------

## Pull / Merge Rule

Before pulling:

- check current branch
- check git status
- do not pull with unrelated local changes unless user approves
- stop on conflict
- explain conflict before resolving

------------------------------------------------------------

## Push Rule

Push is manual.

Before push:

- show last commits
- show status
- confirm branch
- confirm remote
- ask user approval

------------------------------------------------------------

## Rollback Rule

Before rollback:

- identify exact target
- show what will be lost
- ask approval
- prefer safe revert over destructive reset
- never force reset without explicit user approval

------------------------------------------------------------
