---
description: Produce a safe step-by-step plan for the requested task
agent: planner
---

Task: $ARGUMENTS

Use the `planner` agent and `planning` skill from `.opencode/`.

Required steps:

1. Read `.opencode/rules/dispatch-policy.md`, `.opencode/rules/workflow.md`, `.opencode/rules/planning.md`.
2. If the task involves data → also read `.opencode/rules/data-operations.md`.
3. If the task involves git → also read `.opencode/rules/git-operations.md`.
4. If the task involves automation / n8n → also read `.opencode/rules/automation-operations.md`.
5. If the task involves credentials, APIs, financial tools, or external integrations → also read `.opencode/rules/security.md`.

Produce a plan file at `docs/plans/<slug>.md` with sections:

- **Goal** (one sentence)
- **Affected files** (full paths)
- **Affected data** (assets, sensitivity)
- **Steps** (checkbox list, each with verification)
- **Risks** (top 3–5, each with mitigation)
- **Rollback** (per destructive step)
- **Approvals needed** (human-only decisions)

Then return a chat summary: goal, number of steps, top 3 risks, items needing approval.

Do not edit any other files. Do not commit. Do not push.

If the task is ambiguous, ask **one** clarifying question before writing the plan.
