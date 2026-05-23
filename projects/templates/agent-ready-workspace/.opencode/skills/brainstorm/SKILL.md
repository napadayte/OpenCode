---
name: brainstorm
description: "Structured option-generation procedure used BEFORE design or implementation. Produces understanding lock, assumptions, 2-3 options, decision log. Use when: task unclear, multiple approaches possible, architectural choice. На русском: мозговой штурм, варианты, обсудить, накидать идеи. Українською: брейнсторм, варіанти, обговорити."
---

# Brainstorm Skill

A reusable procedure for turning vague ideas into validated direction **before any implementation**.

## When to use

- task is open-ended ("what should I do about X?")
- multiple plausible approaches exist
- architectural / tool / design choice with non-obvious tradeoffs
- workspace setup, automation, or scanner design

## Inputs needed

Identify before starting:
- goal in user's words
- existing context (files, prior decisions)
- constraints (time, scope, environment)
- success criteria
- explicit non-goals

If any is missing, ask **one** question at a time before proceeding.

## Procedure

### 1. Understand context (mandatory first step)

Read what exists: relevant files, prior plans, decision records. Note implicit assumptions. **Do not design yet.**

### 2. Clarify in micro-steps

Ask one question at a time. Prefer multiple-choice over open-ended. Focus on:
- purpose
- users
- constraints
- success criteria
- non-goals

### 3. Non-functional clarification

Explicitly clarify or propose defaults for:
- performance expectations
- scale (users, data, traffic)
- security / privacy
- reliability / availability
- maintenance / ownership

Mark proposed defaults as **assumptions**.

### 4. Understanding lock (hard gate)

Produce a summary block:
- What is being decided
- Why
- Who it's for
- Key constraints
- Explicit non-goals
- Assumptions
- Open questions

Ask user: "Does this accurately reflect your intent?" **Do not proceed until confirmed.**

### 5. Generate 2–3 options

For each:
- short name
- approach summary
- complexity
- extensibility
- risk
- maintenance cost

Lead with your recommendation. YAGNI ruthlessly.

### 6. Decision log

Record:
- what was decided
- alternatives considered
- why this choice

Persist to `docs/decisions/<date>-<slug>.md` if the decision is durable.

## Exit criteria

Exit only when ALL true:
- Understanding lock confirmed by user
- One approach explicitly accepted
- Major assumptions written down
- Top 3 risks acknowledged
- Decision log written

## Output

A short markdown block in chat (and optionally an ADR file) with: goal, assumptions, options compared, recommendation, risks, next step.

## Restrictions

- Do not edit code or implementation files during brainstorm.
- Do not commit.
- Do not push.
- Stop and re-plan if surprises appear.
