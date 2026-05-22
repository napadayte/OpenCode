---
name: document-writing
description: "Workspace documentation conventions: README, runbook, ADR, plan, report, agent/skill doc. Active voice, scannable, no filler. На русском: написать документацию, инструкция, README, runbook, документ. Українською: написати документацію, інструкція."
allowed-tools: Read, Glob, Grep, Edit, Write
risk: low
source: workspace
---

# Document Writing Skill

A reusable procedure for producing maintainable workspace docs.

## When to use

- writing or updating README, runbook, ADR, plan, or agent/skill doc
- adding a new document under `docs/`
- updating documentation after a workspace change

## Inputs needed

- target document path and type
- the change or new content needed
- existing related documents (to keep cross-references intact)

## Document types and required sections

### README
- Purpose (one paragraph)
- Status (Draft / Active / Paused / Deprecated)
- Main documents (links)
- Main folders (one-line description each)
- Safe first prompt (for agent shells)
- Daily workflow (short)
- What not to commit

### Runbook (`docs/runbook.md`)
- Routine operations (each with exact command)
- Failure scenarios (each with detection + recovery)
- Manual stop / kill procedures
- Backup + restore quick reference

### ADR (`docs/decisions/<NNNN>-<slug>.md`)
- Context
- Decision
- Alternatives considered
- Consequences (positive and negative)
- Date and status

### Plan (`docs/plans/<slug>.md`)
- Goal (one sentence)
- Affected files
- Affected data
- Steps (checkbox list with verification)
- Risks
- Rollback
- Approvals needed

### Report (`docs/reports/<date>-<slug>.md`)
- Summary
- What was done
- Verification
- Risks remaining
- Next step

### Agent doc (`.claude/agents/<slug>.md`)
- YAML frontmatter: `name`, `description`, `model`, `color`, `tools:`
- Purpose
- When to use
- Restrictions
- Output format

### Skill doc (`.claude/skills/<slug>/SKILL.md`)
- YAML frontmatter: `name`, `description`, `allowed-tools`, `risk`, `source`
- When to use
- Inputs needed
- Procedure (numbered steps)
- Output
- Restrictions

## Style rules

- Active voice ("Run X" not "X should be run").
- Short paragraphs (2–4 sentences).
- Headings scannable; reader should find an answer in 10 seconds.
- Fenced code blocks for commands.
- Tables for structured comparisons.
- Include the "why" only when non-obvious.
- No motivational filler. No emoji unless requested.
- Use relative links between docs.

## Procedure

### 1. Identify document type and location

Match against the catalog above. Wrong location is a common defect.

### 2. Read the existing version (if any)

Preserve existing structure unless intentionally rewriting.

### 3. Draft or update

Follow the type's required sections. Skip optional sections only when truly empty.

### 4. Cross-reference

- Add link from any index file (e.g. workspace README → new ADR).
- Update related docs that reference the topic.
- For ADRs: increment number based on largest existing number.

### 5. Verify

- All links resolve to existing files (relative paths).
- No leftover `TODO` markers in production docs.
- Style rules above are followed.

## Restrictions

- Do not silently delete existing content during updates.
- Do not create documentation files unless asked or required by the workflow.
- Do not write speculative future-roadmap sections in operational docs.
- Do not paste large blocks of external text without rewriting in workspace style.

## Output

- Files changed
- Cross-references touched
- Risks (e.g. stale links)
- Next recommended step
