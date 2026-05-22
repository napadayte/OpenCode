# How To Add Agents And Skills

## Meaning

```
agent   = who performs the task     → .opencode/agents/<slug>.md
skill   = how to perform the task   → .opencode/skills/<slug>/SKILL.md
rule    = required constraint       → .opencode/rules/<slug>.md
command = reusable slash command    → .opencode/commands/<slug>.md
```

## Where they live

In every generated workspace:

```
.opencode/
├── instructions.md          loaded by OpenCode automatically
├── agents/<slug>.md
├── skills/<slug>/SKILL.md   subdirectory per skill (can grow references/, examples/)
├── rules/<slug>.md
└── commands/<slug>.md

.claude/
└── settings.json            Claude Code runtime permissions only
```

OpenCode is the primary runtime → all content lives under `.opencode/`. `.claude/` keeps only `settings.json` (Claude-specific permissions like denying `Read(./.env)`).

In the global config repo: same layout under `projects/templates/agent-ready-workspace/`.

## Add an agent

Inside a workspace:

```
new-agent-doc <slug>
```

Creates a skeleton at `.opencode/agents/<slug>.md` with YAML frontmatter and placeholders.

Then:

1. Fill the YAML frontmatter. Explicit `tools:` whitelist (least privilege). Read-only agents get only `Read, Glob, Grep, SendMessage`.
2. Write the body: purpose, when to use, restrictions, output format.
3. Mention the agent in `AGENTS.md` and `.opencode/agents/README.md` so it's discoverable.
4. Add an entry under `agent` in workspace `opencode.json` so OpenCode loads it. The agent's `prompt:` is `"Read .opencode/agents/<slug>.md and act as that agent."`

## Add a skill

```
new-skill-doc <slug>
```

Creates `.opencode/skills/<slug>/SKILL.md` with YAML frontmatter and placeholders.

Then:

1. Fill the YAML frontmatter. `risk: high` for procedures touching data, backups, or external services.
2. Write a **distinct, concrete procedure** — not generic boilerplate. If your skill's steps could be copy-pasted into another skill, you don't have a new skill.
3. Mention the skill in `AGENTS.md` and `.opencode/skills/README.md`.

## How to make Claude Code see them too

Claude Code looks by default in `.claude/agents/`, `.claude/skills/<slug>/SKILL.md`, `.claude/commands/`. Our content lives in `.opencode/`, so Claude's agent / skill picker UI won't list the workspace's agents unless we mirror them.

Three ways, simplest first.

### Option 1 — Just use Claude through prompts (default, no mirroring)

Open Claude in the workspace and tell it which file to read:

```
Read .opencode/agents/planner.md and act as that agent.
```

This always works. No mirroring needed. The only downside: Claude's picker UI won't list the workspace's agents.

### Option 2 — Symlinks (Linux / macOS / WSL)

Make `.claude/agents` etc. point to `.opencode/agents` etc. Run once inside a workspace:

```bash
ln -s ../.opencode/agents   .claude/agents
ln -s ../.opencode/skills   .claude/skills
ln -s ../.opencode/commands .claude/commands
ln -s ../.opencode/rules    .claude/rules
```

Claude Code now sees everything in its expected locations. One source of truth — edits go only to `.opencode/`. Commit the symlinks (git tracks them).

On plain Windows (without WSL), symlinks need admin or Developer Mode — usually skip Option 2 there.

### Option 3 — Copy (works everywhere, including plain Windows)

Copy the four folders once, re-copy when content changes. Inside a workspace:

```bash
rm -rf .claude/agents .claude/skills .claude/commands .claude/rules
cp -r  .opencode/agents   .claude/agents
cp -r  .opencode/skills   .claude/skills
cp -r  .opencode/commands .claude/commands
cp -r  .opencode/rules    .claude/rules
```

Drift risk: every edit in `.opencode/` must be re-copied to `.claude/`. Worth it only if you use Claude's picker heavily and can't use symlinks.

## Capture useful external ideas

If you find useful agent rules, workflow notes, or skills in a file:

```
capture-agent-asset <source-file> [asset-name]
```

This:

1. Copies the source to `research/agent-assets/<date>_<name>/source.<ext>` (gitignored).
2. Creates `review.md` with a classification scaffold.
3. Runs a secret-pattern scan, writes results to `secret-scan.txt` if any matched.
4. Suggests the type (agent / skill / mixed / with-rules).

The source is **untrusted intake material**. Do not blindly copy it into the workspace.

## Intake workflow

1. **Capture** via `capture-agent-asset`.
2. **Address secret findings first.** If `secret-scan.txt` exists, treat the source as compromised — review patterns, remove sensitive lines before any further use.
3. **Read** `review.md`.
4. **Analyze** with an agent: `/intake research/agent-assets/<date>_<slug>`.
5. **Extract** only reusable ideas.
6. **Rewrite** in workspace style — short, scannable, concrete steps. No vague filler.
7. **Promote** manually to `.opencode/agents/`, `.opencode/skills/<slug>/SKILL.md`, `.opencode/rules/`, or `.opencode/commands/`.
8. **Check** `git diff`.
9. **Commit** manually.

## What to look for

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

Promote only if the idea is reusable, safer than current behavior, clear, not too narrow, compatible with docs / data / automation work, and rewritten in workspace style.

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
