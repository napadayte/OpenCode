# Skills

Reusable procedures. Each skill is `<slug>/SKILL.md` with YAML frontmatter and an explicit, distinct procedure.

| Skill | Purpose |
|---|---|
| [brainstorm](brainstorm/SKILL.md) | Option-generation procedure with understanding lock |
| [planning](planning/SKILL.md) | Step-by-step plan with verification and rollback |
| [git-safe-commit](git-safe-commit/SKILL.md) | Inspect → secret scan → manual commit |
| [data-inventory](data-inventory/SKILL.md) | Maintain `data/inventory.md` |
| [backup-restore](backup-restore/SKILL.md) | Backup + **verified** restore + runbook entry |
| [n8n-workflow-doc](n8n-workflow-doc/SKILL.md) | Document an n8n workflow safely |
| [security-check](security-check/SKILL.md) | Read-only secret + risk audit |
| [document-writing](document-writing/SKILL.md) | Conventions per doc type |
| [light-code-script](light-code-script/SKILL.md) | Small helper scripts (stdlib first) |
| [stock-scanner-research](stock-scanner-research/SKILL.md) | Research-only scanner (never trades) |

## Format

Each `SKILL.md` starts with YAML frontmatter:

```yaml
---
name: <slug>
description: "<one sentence + trigger words (EN, RU, UA)>"
allowed-tools: <comma-separated list>
risk: <low | medium | high | unknown>
source: <workspace | community | extracted>
---
```

Then the body covers: when to use, inputs needed, procedure (numbered steps), output, restrictions.

## Adding a skill

1. Run `new-skill-doc <slug>` from inside the workspace.
2. Move the created file into a `<slug>/` subdirectory: `<slug>/SKILL.md`.
3. Fill the frontmatter. `risk: high` for any procedure touching data, backups, or external services.
4. Write the procedure as concrete numbered steps — not generic 8-step boilerplate.
5. Update `AGENTS.md` and `.claude/skills/README.md`.

A skill is meaningful only when its procedure is **distinct** from other skills. If you're writing the same generic steps as another skill, that means you don't have a new skill — you have a duplicate of an existing one.
