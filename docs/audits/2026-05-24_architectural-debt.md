# Architectural Debt — 2026-05-24

Status snapshot for the next agent picking up this repo. Records architectural issues that were **intentionally not fixed** in the May 2026 audit cycle, why they were left alone, and what would trigger revisiting them.

This is not a TODO list. Most items here should stay deferred until real user pain shows up. Read this **before** proposing any structural refactor.

---

## 1. Two parallel command/agent ecosystems with the same slash-command names

### What it is

The repo defines `/analyze`, `/plan`, `/review` in **three** different locations with **different** implementations:

| Where | Defined how | Bound to | Used when |
|---|---|---|---|
| `~/.config/opencode/opencode.json` (root) | Inline JSON `command` block | `architect` / `implementer` / `reviewer` (also inline in root JSON) | Opening the config repo itself |
| `~/.config/opencode/commands/` (global, new in PR #26) | Markdown files | No agent — uses `default_agent` | Any folder without a local override |
| `projects/templates/agent-ready-workspace/.opencode/commands/` | Markdown files | `manager` and workspace specialists | Inside a generated workspace |

OpenCode merge order: **project > global**. So:
- In a generated **workspace** → workspace markdown wins → manager-routed flow
- In a generated **code-first project** → no local commands → global markdown wins → generic flow
- In the **config repo itself** → root `opencode.json` inline definitions win → architect-based flow

### Why we did not unify

1. No user reports of confusion. All current users (one human) understand the split.
2. Unification means either (a) renaming root commands to `/analyze-repo` etc. — legitimizes the split forever, or (b) full refactor: move manager + specialists to global, delete workspace-local duplicates, rewrite root config — ~17 files, risk of breaking generation flow.
3. The architectures are not actually the same: a config-repo developer wants `architect`-style direct analysis; a workspace user wants `manager`-routed delegation. The same command name doing different things in different contexts is defensible.

### What would trigger revisit

- A user reports running `/analyze` and getting the wrong shape of output for their context.
- A second generated-workspace flavor is added (third context with same command names) — at that point the ad-hoc split becomes unsustainable.
- The number of workspace-specific commands grows past ~10 — the duplication cost crosses the rewrite cost.

### Recommended approach when the time comes

The "third option" from the audit discussion is on file:
- Move `manager.md` to a workspace-only location (it delegates to workspace-local specialists; it does **not** belong in global).
- Move `architect`/`implementer`/`reviewer` from inline `opencode.json` into `agents/*.md` files.
- Decide per-command whether it's workspace-specific (keep local) or generic (move to global, delete duplicates).
- Force `default_agent` consistency across contexts.

Do **not** do the singular-vs-plural directory rename that came up in discussion. OpenCode supports plural (`agents/`, `commands/`, `skills/`) for both project and global — confirmed against `anomalyco/opencode` docs.

---

## 2. The "empty third door" — `agent-ready-project` template

### What it is

`projects/templates/agent-ready-project/` ships with `.opencode/` containing **only** `instructions.md`. No bundled agents, skills, commands, or rules. After `new-agent-project my-app`, the project depends entirely on the global config at `~/.config/opencode/` for `/analyze`, `/plan`, `/review` and any agent that isn't a shell built-in.

### Why we left it minimal

The template's own `AGENTS.md` says "intentionally minimal" — an authorial signal. As of PR #26 the inheritance contract is **real**:
- Global `commands/` exists (`/analyze`, `/plan`, `/review`).
- Global `agents/` exists (27 subagents).
- `~/.config/opencode/` clone location is documented as **required** in root `README.md`.

So "intentionally minimal" no longer means "intentionally broken if you don't have global setup".

### What would trigger revisit

- Anyone wanting to use `agent-ready-project` **without** the global clone (e.g., shared on a machine that doesn't have the config repo). Currently this fails silently — commands just won't exist.
- A divergent workflow appearing for code-first projects (e.g., a `/test`, `/refactor`, `/migrate` set) that doesn't belong in global because it's only relevant in code contexts.

### Recommended approach when the time comes

Add **code-specific** commands to `agent-ready-project/.opencode/commands/`. The current global commands (`/analyze`, `/plan`, `/review`) are deliberately generic — code-specific commands like `/test`, `/refactor` would live in the template without conflicting.

---

## 3. Hard location dependency on `~/.config/opencode/`

### What it is

Several mechanisms assume the repo is cloned at exactly `~/.config/opencode/`:
- Global `agents/`, `commands/`, `skills/` — loaded by OpenCode from XDG default only.
- `agent-ready-project/AGENTS.md` references this path.
- Several docs in `docs/wiki/` reference this path.

The generator scripts (`tools/bin/*`) resolve their own location via `BASH_SOURCE` and work from any clone — but they're the only thing that does.

### Why we made it a contract rather than removing it

OpenCode itself reads global config from XDG path; we can't make it search elsewhere without forking OpenCode. Documenting the requirement is cheaper than fighting the framework.

### What would trigger revisit

- OpenCode adds `OPENCODE_GLOBAL_CONFIG_DIR` or similar env var.
- A user has a strong reason to put the repo elsewhere (Windows, NixOS readonly /nix/store, corporate /opt enforcement) and the symlink workaround is not enough.

### Recommended approach when the time comes

Document the symlink workaround in `README.md`: `git clone <url> ~/repos/opencode-config && ln -s ~/repos/opencode-config ~/.config/opencode`. OpenCode follows symlinks fine. No code changes needed.

---

## 4. Per-agent `bash` overrides top-level (not merges)

### What it is

In OpenCode, when an agent defines a `permission.bash` block, it **replaces** the top-level `permission.bash` rather than extending it. This was the root cause of PR #25's critical fix: `architect` had `bash: { rg, git status/diff/log }` only, losing `cat`, `find`, `grep` from top-level — its prompt "Analyze the repository" became unworkable.

### Why this is debt, not a fixed bug

PR #25 fixed every existing agent. But future agent additions can re-introduce the same bug — the spec is a footgun. There is no validator that warns when an agent's bash block is narrower than its prompt's needs.

### What would trigger revisit

A new agent is added with a narrow `bash` block and the author doesn't notice it can't read files. Symptom: agent constantly prompts for `cat`/`grep`/`find` despite having "read-only" in description.

### Recommended approach when the time comes

Write a `tools/bin/lint-agent-perms` script: for each `agents/*.md`, parse frontmatter, check that `bash` block includes the cross-platform read set (`cat *`, `type *`, `grep *`, `find *`, `rg *`, `Get-Content *`, `Select-String *`) **if** the agent's prompt mentions analysis/reading/review. Wire it into a pre-commit hook.

---

## 5. Drift risk: `AGENTS.md` (shared) vs `.opencode/instructions.md` (OpenCode-specific)

### What it is

After PR #25 and #26, safety rules live **only** in `AGENTS.md`. `.opencode/instructions.md` is thin, `@AGENTS.md`-imports it, and contains only OpenCode-runtime addendum (WSL preference, `~/code/` convention, wiki sync rule).

But: nothing enforces this separation. A well-meaning future contributor adding "do not delete X" to `instructions.md` would silently re-introduce drift.

### Why we left it as social convention

A check-script for this is harder than for #4 because it'd need to know which rules are universal vs OpenCode-specific. Heuristics over keywords would have false positives.

### What would trigger revisit

A safety-related rule appears in both files with subtly different wording. At that point write the lint.

---

## 6. No verification of OpenCode merge behavior was actually performed

### What it is

Throughout the audit chain we **assumed** OpenCode's config merge behavior based on docs:
- Plural directory names work both globally and locally
- Project commands override global commands
- Inline `command` in `opencode.json` and file in `commands/` coexist (we don't know which wins)
- Plugins load only via `plugin` field in opencode.json, not via `package.json` presence

The docs say all of this. We did **not** run OpenCode and verify. PR #26 removed `package.json` based on docs alone.

### Why we did not verify

The user wanted iteration speed, the docs were unambiguous, the changes are reversible if wrong.

### What would trigger revisit

- A user reports a global command not being picked up.
- A user reports a `package.json` is needed for something we missed.

### Recommended approach when the time comes

Run an actual verification pass in a fresh container:
1. `git clone <repo> ~/.config/opencode`
2. `cd /tmp && new-agent-project test-proj && cd test-proj`
3. `opencode` → try `/analyze`, `@agent-installer`, etc. — record what works.
4. `new-agent-workspace test-ws && cd ../test-ws && opencode` → same.
5. Document the actual behavior in `docs/architecture.md` so the next agent doesn't repeat the assumption.

---

## 7. The `new-agent-workspace` leaves the workspace with no initial commit

### What it is

After `new-agent-workspace foo`, the generated workspace has `git init` run but no first commit. A user opening it with `opencode` and running `/analyze` sees `git status` reporting dozens of untracked files — and the agent may interpret this as "work in progress" rather than "fresh template".

### Why we left it

Cosmetic. The user can `git add -A && git commit -m "initial"` in two seconds. Not worth a PR.

### What would trigger revisit

If an agent's `/analyze` prompt gets misled by the noise more than once. Then add `git add -A && git commit -m "Initial workspace from template"` to the end of `new-agent-workspace` (and `new-agent-project`).

---

## Decision principles applied across the audit

Recorded here so the next agent has the rationale, not just the outcome:

1. **YAGNI > completeness.** Every architectural fix had to defend against "no user reports". Pure-hypothetical problems were declined.
2. **Reversible > optimal.** When two solutions had similar quality, the cheaper-to-undo one won.
3. **Documentation beats code change for ambiguity.** If the question was "is X by design or a bug", document the answer rather than refactor to make the bug impossible.
4. **Hollow promises must die.** Documentation that points at non-existent files, commands, or features is worse than no documentation. Either remove the promise or create the thing it promises.
5. **No new debt to fix old debt.** Every proposed refactor was checked against "does this create a different problem". The `manager.md in global` proposal failed this — it would have referenced non-existent workspace-local agents.

---

## What is **not** in scope of this debt log

- Provider configuration (OpenRouter, Anthropic) — separate concern.
- Wiki RU/EN content — separate concern.
- Per-shell support (Codex CLI, Gemini CLI) beyond what AGENTS.md provides — separate concern.
- The 27 global agents' individual quality — only the loading mechanism is covered here, not their content.

If any of those needs an audit, do it as a separate doc, not by extending this one.
