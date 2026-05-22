# How To Add Agents And Skills

## Meaning

```
agent   = who performs the task     → .claude/agents/<slug>.md
skill   = how to perform the task   → .claude/skills/<slug>/SKILL.md
rule    = required constraint       → .claude/rules/<slug>.md
command = reusable slash command    → .claude/commands/<slug>.md
```

## Where they live

In every generated workspace:

```
.claude/
├── agents/<slug>.md
├── skills/<slug>/SKILL.md     # subdirectory so skills can grow
│                              # references/, examples/, supporting files
├── rules/<slug>.md
├── commands/<slug>.md
└── settings.json
```

In the global OpenCode config repo (this repo) — same layout under `projects/templates/agent-ready-workspace/.claude/`.

## Add an agent

Inside a workspace:

```
new-agent-doc <slug>
```

Creates a skeleton at `.claude/agents/<slug>.md` with YAML frontmatter and placeholders.

Then:

1. Fill the YAML frontmatter. Explicit `tools:` whitelist (principle of least privilege). Read-only agents (critics, reviewers) get only `Read, Glob, Grep, SendMessage`.
2. Write the body: purpose, when to use, restrictions, output format.
3. Mention the agent in `AGENTS.md` and `.claude/agents/README.md` so it's discoverable.
4. If OpenCode should know it, add an entry under `agent` in workspace `opencode.json` — set the agent's `prompt:` to `"Read .claude/agents/<slug>.md and act as that agent."`

## Add a skill

Inside a workspace:

```
new-skill-doc <slug>
```

Creates `.claude/skills/<slug>/SKILL.md` with YAML frontmatter and placeholders.

Then:

1. Fill the YAML frontmatter. `risk: high` for procedures touching data, backups, or external services.
2. Write a **distinct, concrete procedure** — not generic 8-step boilerplate. If your skill's steps could be copy-pasted into another skill, you don't have a new skill.
3. Mention the skill in `AGENTS.md` and `.claude/skills/README.md`.

## Capture useful external ideas

If you find useful agent rules, workflow notes, or skills in a file you downloaded or were shared:

```
capture-agent-asset <source-file> [asset-name]
```

This:

1. Copies the source to `research/agent-assets/<date>_<name>/source.<ext>` (gitignored).
2. Creates `review.md` with a classification scaffold.
3. Runs a secret-pattern scan and writes results to `secret-scan.txt` if any patterns matched.
4. Suggests the type (agent / skill / mixed / with-rules).

The source is **untrusted intake material**. Do not blindly copy it into the workspace.

## Intake workflow

1. **Capture** via `capture-agent-asset`.
2. **Address secret findings first.** If `secret-scan.txt` exists, treat the source as compromised intake — review the patterns and remove sensitive lines before any further use.
3. **Read** `review.md`.
4. **Analyze** with an agent: `/intake research/agent-assets/<date>_<slug>` (the slash command runs the structured extraction).
5. **Extract** only reusable ideas.
6. **Rewrite** in workspace style — short, scannable, concrete steps. No vague filler.
7. **Promote** manually to `.claude/agents/`, `.claude/skills/<slug>/SKILL.md`, or `.claude/rules/`.
8. **Check** `git diff`.
9. **Commit** manually.

## What to look for

Useful patterns in external content:

- "You are..." → potential agent role
- "When to use..." → potential skill or trigger condition
- "Workflow:" / "Pipeline:" / "Steps:" → procedure to extract
- "Output format:" → response shape
- "Ask before..." / "Never..." / "Stop when..." → safety rule
- "Review checklist:" → checklist candidate
- "Rollback:" → recovery step

## What to reject

- framework-specific rules that don't apply
- coding-only rules in a docs-focused workspace
- automatic commit or push behavior
- destructive shortcuts (`rm -rf`, force push, etc.)
- vague motivational text
- copied large external text without rewriting
- secret-handling mistakes

## Promotion rule

Promote only if the idea is:

- reusable
- safer than current behavior
- clear
- not too narrow
- compatible with docs / data / automation work
- written in workspace style after rewrite

## Git rule

Before commit:

```
git status
git diff
```

Never commit:

- secrets
- credentials
- auth files
- raw private source material (already gitignored under `research/agent-assets/*/source.*`)
- backups
- exports
- databases
