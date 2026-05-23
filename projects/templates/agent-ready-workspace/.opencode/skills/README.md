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

Each `SKILL.md` follows the Anthropic Agent Skills spec — required fields only:

```yaml
---
name: <slug>
description: One sentence covering what this skill does AND when to trigger it. Front-load concrete trigger phrases the user is likely to say (EN/RU/UA).
---
```

The body covers: when to use, inputs needed, procedure (numbered steps), output, restrictions. Risk and tool implications belong in the body, not the frontmatter — both OpenCode and Claude Code ignore non-spec fields.

## Adding a skill

1. Run `new-skill-doc <slug>` from inside the workspace.
2. Move the created file into a `<slug>/` subdirectory: `<slug>/SKILL.md`.
3. Fill `name` (must match the directory) and `description` (front-load trigger phrases).
4. Write the procedure as concrete numbered steps — not generic 8-step boilerplate.
5. If the procedure touches data, backups, or external services, document risk and required tools in a body section like `## Risk` and `## Tools used`.
6. Update `AGENTS.md` and this README.

A skill is meaningful only when its procedure is **distinct** from other skills. If you're writing the same generic steps as another skill, that means you don't have a new skill — you have a duplicate of an existing one.
