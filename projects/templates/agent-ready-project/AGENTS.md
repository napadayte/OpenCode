# AGENTS.md

## Project contract

Before changing code:

1. Understand the existing architecture.
2. Prefer small, reviewable changes.
3. Do not introduce new dependencies without explaining why.
4. Do not rewrite large areas unless explicitly requested.
5. Keep public APIs backward compatible unless the task says otherwise.

## Workflow

Default workflow:

1. Explore relevant files.
2. Explain the plan.
3. Make minimal changes.
4. Run the smallest relevant verification.
5. Summarize:
   - changed files
   - why changed
   - how verified
   - remaining risks

## Safety

Never run destructive commands without explicit approval.

Forbidden unless explicitly requested:

- `rm -rf`
- force push
- deleting migrations
- dropping databases
- changing secrets
- changing production config
- broad formatting of unrelated files

## Code style

Follow the existing project style.

Do not add comments that merely repeat the code.

Prefer clear names over clever abstractions.

## Testing

When implementing:

- add or update tests for changed behavior when relevant
- run the smallest relevant test first
- only run full test suite when necessary or requested

## Git

Do not push.

Do not commit unless explicitly requested.

Show `git diff` summary after changes.

## Architecture

Keep architecture documented in `docs/architecture.md`.

For important decisions, add an ADR in `docs/decisions/`.
