---
name: planning
description: "Turn an approved direction into a small, verifiable step-by-step plan with affected files, verification, and rollback. Use AFTER brainstorm, BEFORE implementation. На русском: планирование, расписать шаги, декомпозиция, риски, план. Українською: планування, кроки реалізації."
allowed-tools: Read, Glob, Grep, Write
risk: low
source: workspace
---

# Planning Skill

A reusable procedure for producing a concrete, reviewable plan before any change.

## When to use

- task touches more than 3 files
- data, database, backup, or restore involved
- automation, workflow, or template change
- multi-step work with non-obvious ordering
- any risky task

## Inputs needed

- approved direction (from brainstorm or user)
- known constraints
- list of files / data that will likely be touched

## Procedure

### 1. State goal in one sentence

If you can't, the goal isn't clear enough — go back to brainstorm.

### 2. Map affected surface

List by category:
- files (full paths)
- data (datasets, databases, exports, backups)
- external services (APIs, n8n nodes, Docker volumes)
- agents / skills / rules

### 3. Break into small steps

Each step must be:
- specific (concrete action, not "set up X")
- 2–10 minutes of work
- independently verifiable

Avoid steps like "configure everything" or "test the system."

### 4. Define verification per step

For each step:
- What command to run, or what to check.
- What the expected output is.
- How to know it failed.

### 5. Define rollback

For each destructive step:
- What was backed up
- Exact restore command
- How to verify restore worked

If a step has no rollback path, mark it **irreversible** and flag for approval.

### 6. List risks

Top 3–5 risks. For each:
- what can go wrong
- impact
- mitigation

### 7. Flag approvals

List human-only decisions. Common: delete data, push to remote, change credentials, modify global config.

## Output

Plan file at `docs/plans/<slug>.md` with these sections in order:

```
# <Plan Title>

## Goal
One sentence.

## Affected files
- path/one
- path/two

## Affected data
- asset / location / sensitivity

## Steps
- [ ] 1. <action> → verify: <how>
- [ ] 2. <action> → verify: <how>

## Risks
- <risk>: <mitigation>

## Rollback
- <what reverts each destructive step>

## Approvals needed
- <decision>
```

Plus a chat summary: goal, # of steps, top 3 risks, items needing approval.

## Restrictions

- Maximum ~10 tasks per plan. If more, split into multiple plans.
- Do not implement during planning.
- Update the plan as steps complete (`[x]` checkmark).
- Do not commit or push.
