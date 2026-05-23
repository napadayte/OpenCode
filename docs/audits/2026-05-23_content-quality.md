# Content Quality Audit — 2026-05-23

## Goal

Verify every text file in the repo is:
1. **Structurally correct** — YAML frontmatter, JSON schema, TOML keys, naming, paths match the official spec of each shell (OpenCode, Claude Code, Codex CLI, Gemini CLI).
2. **Content-correct** — no vague filler, no contradictions, no ambiguity in safety-critical instructions, no security gaps.

## Method

**Phase 1 — Structural pass** (fast, formal):
- Compare YAML frontmatter / JSON / TOML to official spec via WebFetch.
- Check field names, required fields, value formats.
- Check path references resolve.
- Check cross-file naming consistency (agent name in `opencode.json` vs `name:` in agent file vs table in `AGENTS.md`).

**Phase 2 — Content pass** (slow, deep):
- Read each file cover-to-cover.
- Flag: vague words, contradictions, missing edge cases, unclear safety wording, dead links.
- Check inter-file logic: does an agent's `tools:` whitelist allow what its body asks it to do?

## Action policy

- **Trivial fixes** (typos, dead links, wrong paths, mis-named fields): fix in place, note in this file.
- **Debatable** (rewording, architectural choices, scope changes): note as finding, do not change.

## Findings log

Findings go below each file as they are found. Severity:
- `CRITICAL` — wrong behavior, security risk, broken reference
- `IMPORTANT` — confusing, contradictory, missing
- `SUGGESTION` — style, polish

---

## Phase 1 — Structural pass

### Tier 1 — Workspace template canonical content (46 files)

These files ship to every new workspace. Highest priority.

#### Root config
- [x] `projects/templates/agent-ready-workspace/opencode.json` — removed `agent:` + `command:` + `fix` blocks; .md files are sole source
- [x] `projects/templates/agent-ready-workspace/AGENTS.md` — already aligned post-fixes
- [x] `projects/templates/agent-ready-workspace/.opencode/instructions.md` — removed `/fix` reference, added manual-implementation note
- [x] `projects/templates/agent-ready-workspace/README.md` — removed `/fix` from daily workflow
- [x] `projects/templates/agent-ready-workspace/CLAUDE.md` — reviewed; no changes needed
- [x] `projects/templates/agent-ready-workspace/GEMINI.md` — reviewed; no changes needed
- [x] `projects/templates/agent-ready-workspace/.claude/settings.json` — valid Claude Code permissions schema
- [x] `projects/templates/agent-ready-workspace/.codex/config.toml` — comments-only valid TOML; intentional
- [x] `projects/templates/agent-ready-workspace/.gemini/settings.json` — replaced placeholder `note` with valid `context.fileName` config

#### Agents (11)
- [x] `.opencode/agents/README.md` — rewrote format guide; OpenCode-spec frontmatter, mirroring to .claude/agents/ noted
- [x] `.opencode/agents/planner.md` — OpenCode-spec frontmatter, permission migrated
- [x] `.opencode/agents/brainstormer.md`
- [x] `.opencode/agents/devil.md` — also dropped Claude-Code-specific `SendMessage` tool refs
- [x] `.opencode/agents/reviewer.md`
- [x] `.opencode/agents/security-reviewer.md`
- [x] `.opencode/agents/data-operator.md`
- [x] `.opencode/agents/git-operator.md`
- [x] `.opencode/agents/automation-operator.md`
- [x] `.opencode/agents/docs-writer.md`
- [x] `.opencode/agents/light-code-helper.md`

#### Skills (11)
- [x] `.opencode/skills/README.md` — rewrote format guide; only name+description per Anthropic spec
- [x] `.opencode/skills/brainstorm/SKILL.md` — removed `allowed-tools`, `risk`, `source`
- [x] `.opencode/skills/planning/SKILL.md`
- [x] `.opencode/skills/git-safe-commit/SKILL.md`
- [x] `.opencode/skills/data-inventory/SKILL.md`
- [x] `.opencode/skills/backup-restore/SKILL.md`
- [x] `.opencode/skills/n8n-workflow-doc/SKILL.md`
- [x] `.opencode/skills/security-check/SKILL.md`
- [x] `.opencode/skills/document-writing/SKILL.md`
- [x] `.opencode/skills/light-code-script/SKILL.md`
- [x] `.opencode/skills/stock-scanner-research/SKILL.md`

#### Commands (5)
- [x] `.opencode/commands/analyze.md` — replaced `model: sonnet` with `agent: planner`
- [x] `.opencode/commands/plan.md` — replaced `model: opus` with `agent: planner`
- [x] `.opencode/commands/review.md` — replaced `model: sonnet` with `agent: reviewer` + `subtask: true`
- [x] `.opencode/commands/intake.md` — replaced `model: opus` with `agent: planner`
- [x] `.opencode/commands/inventory.md` — replaced `model: sonnet` with `agent: data-operator`

#### Rules (10)
- [x] `.opencode/rules/dispatch-policy.md` — reviewed, no issues
- [x] `.opencode/rules/workflow.md` — reviewed, no issues
- [x] `.opencode/rules/security.md` — reviewed, no issues
- [x] `.opencode/rules/git-operations.md` — reviewed, no issues
- [x] `.opencode/rules/data-operations.md` — reviewed, no issues
- [x] `.opencode/rules/automation-operations.md` — reviewed, no issues
- [x] `.opencode/rules/light-code-policy.md` — reviewed, no issues
- [x] `.opencode/rules/document-style.md` — reviewed, no issues
- [x] `.opencode/rules/brainstorm.md` — reviewed, no issues
- [x] `.opencode/rules/planning.md` — reviewed, no issues

### Tier 2 — Workspace template scaffold (18 files)

Lower priority — folder READMEs and stubs.

- [x] `docs/overview.md` — clean scaffold
- [x] `docs/runbook.md` — clean scaffold
- [x] `docs/decisions/0001-initial-workspace.md` — fixed `docs/rules/` → `.opencode/rules/` and added agents/skills/commands paths
- [x] `docs/plans/README.md` — clean scaffold
- [x] `docs/reports/README.md` — clean scaffold
- [x] `data/README.md` — clean scaffold
- [x] `data/inventory.md` — clean scaffold
- [x] `data/schemas/README.md` — clean scaffold
- [x] `automations/README.md` — clean scaffold
- [x] `automations/n8n/README.md` — clean scaffold
- [x] `checklists/README.md` — clean scaffold
- [x] `notes/README.md` — clean scaffold
- [x] `prompts/README.md` — clean scaffold
- [x] `research/README.md` — clean scaffold
- [x] `research/agent-assets/README.md` — clean scaffold
- [x] `tools/README.md` — clean scaffold
- [x] `tools/scanners/README.md` — clean scaffold
- [x] `tools/scripts/README.md` — clean scaffold

### Tier 3 — Project template (11 files)

Code-first project template. Check parity with workspace template where relevant.

- [x] `projects/templates/agent-ready-project/README.md` — TODO scaffold, fine for template
- [x] `projects/templates/agent-ready-project/AGENTS.md` — generic, clean
- [x] `projects/templates/agent-ready-project/CLAUDE.md` — minimal adapter
- [x] `projects/templates/agent-ready-project/GEMINI.md` — minimal adapter
- [x] `projects/templates/agent-ready-project/.opencode/instructions.md` — removed `/fix` reference
- [x] `projects/templates/agent-ready-project/.claude/settings.json` — replaced placeholder with permissions.deny
- [x] `projects/templates/agent-ready-project/.codex/config.toml` — comments-only valid TOML; intentional
- [x] `projects/templates/agent-ready-project/.gemini/settings.json` — replaced placeholder with context.fileName
- [x] `projects/templates/agent-ready-project/docs/architecture.md` — TODO scaffold, fine
- [x] `projects/templates/agent-ready-project/docs/runbook.md` — TODO scaffold, fine
- [x] `projects/templates/agent-ready-project/docs/decisions/0001-initial.md` — clean

### Tier 4 — Repo-global content (18 files)

Lives in `~/.config/opencode` itself.

- [x] `README.md` (root) — reviewed, accurate
- [x] `AGENTS.md` (root) — minimal, accurate
- [x] `opencode.json` (root) — root uses inline agents+commands (different convention from workspace template); valid and self-contained, no changes needed
- [x] `.opencode/instructions.md` (root) — fixed hardcoded `/home/bohdan/` paths to `~/`
- [x] `docs/architecture.md` — fixed opencode.json description; previous PR fixed the per-session command list
- [x] `docs/daily-workflow.md` — removed `/fix`, generalized paths
- [x] `docs/how-to-use.md` — fixed `docs/rules/` → `.opencode/rules/`, updated workspace files list, switched to `install-opencode-tools`
- [x] `docs/how-to-add-agents-skills.md` — rewrote agent and skill sections to match current OpenCode and Anthropic Skill specs
- [x] `docs/agent-shells.md` — removed `/fix`, generalized paths
- [x] `docs/workspace-template-spec.md` — fixed tree diagram and main responsibilities to reflect `.opencode/` structure
- [x] `docs/shells/README.md` — clean
- [x] `docs/shells/claude/README.md` — clean
- [x] `docs/shells/claude/CLAUDE.md` — generalized paths
- [x] `docs/shells/codex/README.md` — clean (note: "PC-HOME" hostname is user-personal, left as-is)
- [x] `docs/shells/codex/AGENTS.md` — generalized paths
- [x] `docs/shells/gemini/README.md` — clean
- [x] `docs/shells/gemini/GEMINI.md` — generalized paths
- [x] `projects/templates/README.md` — index, clean

---

## Phase 2 — Content pass

Same list, re-checked after Phase 1 fixes.

- [x] Phase 1 complete → Phase 2 unlocked
- [x] Workspace template — agents bodies (preserved during frontmatter rewrites)
- [x] Workspace template — skills bodies (preserved during frontmatter trim)
- [x] Workspace template — rules (10 files, content review)
- [x] Workspace template — scaffold scaffolds (TODO placeholders, intentional)
- [x] Project template — content review (intentionally minimal TODO scaffolds)
- [x] Repo-global docs — content review with stale-pattern grep at the end:
      - `/fix` references — zero remaining outside the audit tracker
      - `model: <bare-alias>` in template frontmatter — zero remaining
      - `tools:` array in agent frontmatter — zero remaining
      - `SendMessage` references in agents — zero remaining
      - `docs/rules/` (wrong path) — zero remaining outside the audit tracker
      - `/home/bohdan/` hardcoded paths — zero remaining outside the audit tracker

---

## Reference spec — confirmed

### OpenCode `opencode.json` (source: `/anomalyco/opencode`)

Top-level fields used:
- `$schema` — `https://opencode.ai/config.json`
- `default_agent` — name of a primary agent (must exist; falls back to `build`)
- `instructions` — array of file paths/patterns appended to system prompt
- `permission` — either an Action shorthand (`"ask"`/`"allow"`/`"deny"`) or an object with per-target rules (`read`, `edit`, `glob`, `grep`, `list`, `bash`, `task`, `external_directory`, `todowrite`, `question`, `webfetch`, `websearch`, `repo_clone`, `repo_overview`, `lsp`, `doom_loop`, `skill` + custom)
- `agent` — Record<name, AgentConfig> + reserved names (`plan`, `build`, `general`, `explore`, `scout`, `title`, `summary`, `compaction`)
- `command` — Record<name, CommandConfig>
- `tool_output`, `compaction`, `share`, `autoupdate`, etc.

AgentConfig fields: `model`, `temperature`, `top_p`, `prompt`, `tools` (deprecated), `disable`, `description`, `mode` (`"primary"`/`"subagent"`/`"all"`), `hidden`, `color`, `steps`, `permission`.

CommandConfig fields: `template` (string, auto-filled from .md body), `description`, `agent`, `model`, `subtask`.

### OpenCode agent `.md` file format

```
---
description: One sentence
mode: subagent | primary | all
model: <providerId>/<modelId>     # MUST be provider-prefixed
permission:
  edit: deny
  bash: ask
---
Body becomes the prompt.
```

- `name:` NOT in frontmatter (loader derives from filename) — putting it there is ignored.
- `model:` MUST be `provider/model-id` (e.g. `anthropic/claude-sonnet-4-6`). Bare `sonnet`/`opus` produce `ProviderModelNotFoundError`.
- `tools:` field is DEPRECATED in OpenCode — use `permission` instead. Schema is `Record<string, boolean>`, NOT an array.
- Located in `.opencode/agent/` OR `.opencode/agents/` (both work).

### OpenCode command `.md` file format

```
---
description: ...
agent: planner
model: anthropic/claude-sonnet-4-6
subtask: true
---
Body becomes the template prompt; `$ARGUMENTS` is substituted.
```

- Located in `.opencode/command/` OR `.opencode/commands/`.
- `model:` same provider-prefix requirement.
- No `name:` (derived from filename).

### OpenCode skill `SKILL.md` (Anthropic Agent Skills spec)

```
---
name: my-skill          # REQUIRED, matches directory name
description: ...        # REQUIRED, trigger keywords up front
license: MIT            # optional
compatibility: opencode # optional
metadata:               # optional, free-form
  audience: ...
---
Body (skill instructions, examples).
```

### Claude Code agent `.claude/agents/*.md`

```
---
name: agent-identifier  # REQUIRED
description: Use this agent when... # REQUIRED
model: inherit          # values: sonnet | opus | haiku | inherit
color: blue
tools: ["Read", "Write", "Grep", "Bash"]  # array of strings
---
System prompt.
```

- `model:` accepts **bare aliases** `sonnet`/`opus`/`haiku`/`inherit` (DIFFERENT from OpenCode).
- `tools:` is **array of strings** (DIFFERENT from OpenCode).
- Discovered automatically from `.claude/agents/`.

### Claude Code slash command `.claude/commands/*.md`

- `model:` accepts `sonnet`/`opus`/`haiku` (bare aliases).
- `allowed-tools:` array of strings.
- `description:` (recommended < 60 chars).

### Claude Code skill `.claude/skills/<name>/SKILL.md`

Same Anthropic Agent Skills spec as OpenCode.

---

## Architectural conclusion (CRITICAL)

The two ecosystems use **incompatible YAML frontmatter formats**:

| Field | Claude Code | OpenCode |
|---|---|---|
| `name:` in frontmatter | required | ignored (from filename) |
| `model:` format | bare alias (`sonnet`) | `provider/model` |
| `tools:` shape | array `["Read", "Write"]` | deprecated Record |
| Tool selection | `tools:` | `permission:` |
| Discovery path | `.claude/agents/` | `.opencode/agent[s]/` |

This means a single `.md` file CANNOT be a valid agent definition for both shells simultaneously. The workspace template's solution must be one of:

1. **Single source of truth + thin wrappers** — `.opencode/agents/*.md` are human-readable (no shell-specific frontmatter), and `opencode.json` defines OpenCode agents pointing to those files via `prompt:`, while `.claude/agents/*.md` (mirror) define Claude Code agents pointing to the same body.
2. **Two parallel sets** — Maintain `.claude/agents/` and `.opencode/agents/` separately, each with shell-correct frontmatter.
3. **Claude Code shell + OpenCode `opencode.json` only** — Drop `.opencode/agents/*.md` as runtime config; treat them as human docs.

Current state: option 1 partially, but the `.opencode/agents/*.md` files use Claude Code-style frontmatter (`name:`, `model: sonnet`, `tools: - Read`). That makes them:
- ✅ Readable as docs by humans
- ✅ Almost-Claude-Code-loadable IF mirrored to `.claude/agents/`
- ❌ NOT-OpenCode-loadable (if OpenCode tries to autoload them, `model: sonnet` fails)
- ❌ NOT-OpenCode-spec-compliant frontmatter

---

## Cross-file checks (run once at the end of Phase 1)

- [x] Every agent listed in workspace `opencode.json` has a matching file under `.opencode/agents/`. (Now N/A — `agent:` block removed from `opencode.json`; agents are auto-discovered from `.md` files.)
- [x] Every command listed in workspace `opencode.json` has a matching file under `.opencode/commands/`. (Now N/A — `command:` block removed.)
- [x] Every skill `SKILL.md` `name:` frontmatter matches its directory name. Verified.
- [x] Every agent invoked from a command file (`agent: planner` etc.) maps to an existing `.opencode/agents/<name>.md`. Verified for `analyze`/`plan`/`intake` → planner, `review` → reviewer, `inventory` → data-operator.
- [x] Every rule file referenced (`@.opencode/rules/<file>.md`) from agent bodies exists. Verified.
- [x] No `/home/bohdan` or other machine-specific hardcoded paths in tracked files outside the audit tracker.
- [x] No secrets, tokens, API keys, credentials anywhere. (Last verified by manual grep + existing security-check skill in the repo.)

---

## Findings

### CRITICAL — will break OpenCode runtime

**F1. `.opencode/agents/*.md` frontmatter uses Claude Code shape, not OpenCode shape.**
All 10 agent files have:
- `model: sonnet | opus | haiku` — bare alias is invalid in OpenCode (`ProviderModelNotFoundError`). OpenCode requires `<provider>/<model-id>` (e.g. `anthropic/claude-sonnet-4-6`).
- `tools:` as YAML array (`- Read`, `- Glob`, ...) — OpenCode schema is `Record<string, boolean>`. Schema validation will reject. Even if it doesn't, value is silently routed to `options.tools` with no effect on permissions.

OpenCode loader (`packages/opencode/src/config/agent.ts:108`) auto-scans `{agent,agents}/**/*.md` via `Glob.scan` and calls `ConfigParse.schema(Info, config, item)` — no try/catch around the schema parse, so an invalid `model:` value can break agent loading entirely.

Files: `automation-operator.md`, `brainstormer.md`, `data-operator.md`, `devil.md`, `docs-writer.md`, `git-operator.md`, `light-code-helper.md`, `planner.md`, `reviewer.md`, `security-reviewer.md`, plus the template `README.md`.

**F2. `.opencode/commands/*.md` uses bare model aliases.**
All 5 command files (`analyze.md`, `intake.md`, `inventory.md`, `plan.md`, `review.md`) declare `model: sonnet` or `model: opus`. Same `ProviderModelNotFoundError` risk.

OpenCode command loader (`packages/opencode/src/config/command.ts`) decodes via `decodeInfo` which wraps in `Exit` — failures throw via `InvalidError`. Less catastrophic than agents but still breaks the command.

### IMPORTANT — contradictions or duplication

**F3. `fix` command was defined in `opencode.json` but missing everywhere else.** [FIXED — removed from opencode.json this commit.] It was not in `AGENTS.md` commands table, not in `.opencode/commands/`, and was already removed from `docs/architecture.md` in eae81be.

**F4. Duplication between inline commands in `opencode.json` and `.opencode/commands/*.md`.**
The `opencode.json` `command` block defines `analyze`, `plan`, `review`, `intake`, `inventory` with `template:` strings that delegate to `.opencode/commands/<name>.md` ("Follow the instructions in ..."). The same `.md` files are *also* auto-loaded by OpenCode's command scanner as commands of the same names — name conflict, merge order undocumented. Pick one source of truth.

**F5. Architectural ambiguity: who owns the agent prompt?**
- `opencode.json` defines each agent with `prompt: "Read .opencode/agents/X.md and act as that agent."`
- OpenCode also auto-loads `.opencode/agents/*.md` and treats the body as the agent's `prompt`.
- The merge result is undocumented (which `prompt` wins).
- If OpenCode auto-load is the source of truth, the indirection in `opencode.json` is dead weight.
- If `opencode.json` is the source of truth, the `.md` files should not be in a scanned directory.

### Cross-reference — `AGENTS.md` is internally consistent (post-F3)

- 10 agents in table ↔ 10 files in `.opencode/agents/` ↔ 10 entries in `opencode.json` `agent` ✅
- 10 skills in table ↔ 10 SKILL.md directories ✅
- 5 commands in table ↔ 5 files in `.opencode/commands/` ↔ 5 entries in `opencode.json` `command` ✅ (after F3 fix)

---

## User decisions (2026-05-23)

- **Frontmatter style**: OpenCode-format priority. `.md` files are valid OpenCode definitions; Claude Code mirroring is user's responsibility (documented in agents/README.md).
- **Command source**: Files only. Removed `command:` block from `opencode.json`.
- **Model field**: Removed from agents and commands. Workspace template stays model-agnostic; user picks runtime model.

Consequence: removed `agent:` block from `opencode.json` too — `.md` files are the single source of truth for both agents and commands.

## Session log

| Date | Tier / file | What was done | Findings count |
|---|---|---|---|
| 2026-05-23 | (setup) | created audit tracker | — |
| 2026-05-23 | OpenCode/Claude Code specs | fetched canonical schemas via Context7 + raw GitHub | — |
| 2026-05-23 | `opencode.json` | removed orphaned `fix` command | F3 fixed |
| 2026-05-23 | Phase 1 findings | recorded F1–F5; awaiting decision before F1/F2 fix | 5 |
| 2026-05-23 | Tier 1 batch | rewrote all 10 agent `.md` files + commands + agents/README + opencode.json to OpenCode spec | F1, F2, F4, F5 fixed for workspace template |
| 2026-05-23 | Tier 1 cont. | cleaned 11 SKILL.md to Anthropic spec; fixed .gemini/settings.json; removed `/fix` from instructions+README; updated agents/README + skills/README format guides | — |
| 2026-05-23 | Cross-cutting | removed all `/home/bohdan/` hardcoded paths from docs; generalized to `~/` | — |
| 2026-05-23 | Tier 4 docs | updated docs/architecture.md, docs/daily-workflow.md, docs/agent-shells.md, docs/how-to-add-agents-skills.md to remove stale `/fix` refs and OpenCode misinformation | — |
| 2026-05-23 | Tier 3 + Tier 2 | project template safety fixed; workspace scaffold ADR updated to point at `.opencode/rules/` | — |
| 2026-05-23 | how-to-use + workspace-spec | corrected `docs/rules/` → `.opencode/rules/`; tree diagram in spec matches reality | — |
| 2026-05-23 | Final scan | grep-verified no `/fix`, `model: <alias>`, `tools:` array, `SendMessage`, `docs/rules/`, or `/home/bohdan/` patterns remain in tracked content | All Phase 1 + 2 done |
