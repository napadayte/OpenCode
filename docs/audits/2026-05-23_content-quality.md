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
- [ ] `projects/templates/agent-ready-workspace/opencode.json`
- [ ] `projects/templates/agent-ready-workspace/AGENTS.md`
- [ ] `projects/templates/agent-ready-workspace/.opencode/instructions.md`
- [ ] `projects/templates/agent-ready-workspace/README.md`
- [ ] `projects/templates/agent-ready-workspace/CLAUDE.md`
- [ ] `projects/templates/agent-ready-workspace/GEMINI.md`
- [ ] `projects/templates/agent-ready-workspace/.claude/settings.json`
- [ ] `projects/templates/agent-ready-workspace/.codex/config.toml`
- [ ] `projects/templates/agent-ready-workspace/.gemini/settings.json`

#### Agents (11)
- [ ] `.opencode/agents/README.md`
- [ ] `.opencode/agents/planner.md`
- [ ] `.opencode/agents/brainstormer.md`
- [ ] `.opencode/agents/devil.md`
- [ ] `.opencode/agents/reviewer.md`
- [ ] `.opencode/agents/security-reviewer.md`
- [ ] `.opencode/agents/data-operator.md`
- [ ] `.opencode/agents/git-operator.md`
- [ ] `.opencode/agents/automation-operator.md`
- [ ] `.opencode/agents/docs-writer.md`
- [ ] `.opencode/agents/light-code-helper.md`

#### Skills (11)
- [ ] `.opencode/skills/README.md`
- [ ] `.opencode/skills/brainstorm/SKILL.md`
- [ ] `.opencode/skills/planning/SKILL.md`
- [ ] `.opencode/skills/git-safe-commit/SKILL.md`
- [ ] `.opencode/skills/data-inventory/SKILL.md`
- [ ] `.opencode/skills/backup-restore/SKILL.md`
- [ ] `.opencode/skills/n8n-workflow-doc/SKILL.md`
- [ ] `.opencode/skills/security-check/SKILL.md`
- [ ] `.opencode/skills/document-writing/SKILL.md`
- [ ] `.opencode/skills/light-code-script/SKILL.md`
- [ ] `.opencode/skills/stock-scanner-research/SKILL.md`

#### Commands (5)
- [ ] `.opencode/commands/analyze.md`
- [ ] `.opencode/commands/plan.md`
- [ ] `.opencode/commands/review.md`
- [ ] `.opencode/commands/intake.md`
- [ ] `.opencode/commands/inventory.md`

#### Rules (10)
- [ ] `.opencode/rules/dispatch-policy.md`
- [ ] `.opencode/rules/workflow.md`
- [ ] `.opencode/rules/security.md`
- [ ] `.opencode/rules/git-operations.md`
- [ ] `.opencode/rules/data-operations.md`
- [ ] `.opencode/rules/automation-operations.md`
- [ ] `.opencode/rules/light-code-policy.md`
- [ ] `.opencode/rules/document-style.md`
- [ ] `.opencode/rules/brainstorm.md`
- [ ] `.opencode/rules/planning.md`

### Tier 2 — Workspace template scaffold (18 files)

Lower priority — folder READMEs and stubs.

- [ ] `docs/overview.md`
- [ ] `docs/runbook.md`
- [ ] `docs/decisions/0001-initial-workspace.md`
- [ ] `docs/plans/README.md`
- [ ] `docs/reports/README.md`
- [ ] `data/README.md`
- [ ] `data/inventory.md`
- [ ] `data/schemas/README.md`
- [ ] `automations/README.md`
- [ ] `automations/n8n/README.md`
- [ ] `checklists/README.md`
- [ ] `notes/README.md`
- [ ] `prompts/README.md`
- [ ] `research/README.md`
- [ ] `research/agent-assets/README.md`
- [ ] `tools/README.md`
- [ ] `tools/scanners/README.md`
- [ ] `tools/scripts/README.md`

### Tier 3 — Project template (11 files)

Code-first project template. Check parity with workspace template where relevant.

- [ ] `projects/templates/agent-ready-project/README.md`
- [ ] `projects/templates/agent-ready-project/AGENTS.md`
- [ ] `projects/templates/agent-ready-project/CLAUDE.md`
- [ ] `projects/templates/agent-ready-project/GEMINI.md`
- [ ] `projects/templates/agent-ready-project/.opencode/instructions.md`
- [ ] `projects/templates/agent-ready-project/.claude/settings.json`
- [ ] `projects/templates/agent-ready-project/.codex/config.toml`
- [ ] `projects/templates/agent-ready-project/.gemini/settings.json`
- [ ] `projects/templates/agent-ready-project/docs/architecture.md`
- [ ] `projects/templates/agent-ready-project/docs/runbook.md`
- [ ] `projects/templates/agent-ready-project/docs/decisions/0001-initial.md`

### Tier 4 — Repo-global content (18 files)

Lives in `~/.config/opencode` itself.

- [ ] `README.md` (root)
- [ ] `AGENTS.md` (root)
- [ ] `opencode.json` (root)
- [ ] `.opencode/instructions.md` (root)
- [ ] `docs/architecture.md`
- [ ] `docs/daily-workflow.md`
- [ ] `docs/how-to-use.md`
- [ ] `docs/how-to-add-agents-skills.md`
- [ ] `docs/agent-shells.md`
- [ ] `docs/workspace-template-spec.md`
- [ ] `docs/shells/README.md`
- [ ] `docs/shells/claude/README.md`
- [ ] `docs/shells/claude/CLAUDE.md`
- [ ] `docs/shells/codex/README.md`
- [ ] `docs/shells/codex/AGENTS.md`
- [ ] `docs/shells/gemini/README.md`
- [ ] `docs/shells/gemini/GEMINI.md`
- [ ] `projects/templates/README.md`

---

## Phase 2 — Content pass

Same list, re-checked after Phase 1 fixes. Phase 2 starts only when Phase 1 is complete.

- [ ] Phase 1 complete → unlock Phase 2

---

## Reference spec URLs

Filled as fetched (caching here so we don't refetch per file).

- OpenCode config: <pending fetch>
- OpenCode agents: <pending fetch>
- Claude Code settings.json: <pending fetch>
- Claude Code agents: <pending fetch>
- Claude Code skills (SKILL.md): <pending fetch>
- Claude Code slash commands: <pending fetch>
- Codex CLI config.toml: <pending fetch>
- Codex CLI AGENTS.md: <pending fetch>
- Gemini CLI settings.json: <pending fetch>

---

## Cross-file checks (run once at the end of Phase 1)

- [ ] Every agent listed in workspace `opencode.json` has a matching file under `.opencode/agents/`.
- [ ] Every command listed in workspace `opencode.json` has a matching file under `.opencode/commands/`.
- [ ] Every agent file `name:` frontmatter matches its filename slug.
- [ ] Every skill `SKILL.md` `name:` frontmatter matches its directory name.
- [ ] Every command file referenced by `.opencode/commands/*.md` (e.g. "Use the `planner` agent") points to an existing agent.
- [ ] Every rule file referenced by AGENTS.md and command files exists.
- [ ] Every path mentioned in any doc resolves (no dead refs).
- [ ] No `/home/bohdan` or other machine-specific hardcoded paths.
- [ ] No secrets, tokens, API keys, credentials anywhere.

---

## Session log

| Date | Tier / file | What was done | Findings count |
|---|---|---|---|
| 2026-05-23 | (setup) | created audit tracker | — |
