# How To Add Agents And Skills

------------------------------------------------------------

## 1. Meaning

Agent:

    who performs the task

Skill:

    how to perform the task

Rule:

    required constraint or safety boundary

------------------------------------------------------------

## 2. Where They Live

In every generated workspace:

    agents/
    skills/
    docs/rules/

In the global OpenCode config repo:

    ~/.config/opencode

Template path:

    ~/.config/opencode/projects/templates/agent-ready-workspace

------------------------------------------------------------

## 3. How To Add Agent Manually

Inside a workspace:

    new-agent-doc <agent-slug>

Example:

    new-agent-doc security-reviewer

Then edit:

    agents/security-reviewer.md

Also mention the agent in:

    AGENTS.md
    docs/rules/dispatch-policy.md

------------------------------------------------------------

## 4. How To Add Skill Manually

Inside a workspace:

    new-skill-doc <skill-slug>

Example:

    new-skill-doc n8n-workflow-doc

Then edit:

    skills/n8n-workflow-doc.md

Also mention the skill in:

    AGENTS.md
    CLAUDE.md
    GEMINI.md
    .opencode/instructions.md
    .codex/config.toml

------------------------------------------------------------

## 5. How To Capture Useful External Ideas

If you find useful agent rules, workflow notes, or skills in a file:

    capture-agent-asset <source-file> [asset-name]

Example:

    capture-agent-asset ~/Downloads/claude-rules.md claude-rules

This creates:

    research/agent-assets/<date>_<name>/review.md
    research/agent-assets/<date>_<name>/source.*

The source is treated as raw intake material.

Do not blindly copy it into the system.

------------------------------------------------------------

## 6. Intake Workflow

1. Capture the source.
2. Read review.md.
3. Ask an agent to analyze the source.
4. Extract only reusable ideas.
5. Rewrite in our style.
6. Add as agent, skill, or rule.
7. Check git diff.
8. Commit manually.

------------------------------------------------------------

## 7. What To Look For

Useful patterns:

- You are...
- Use this agent when...
- Workflow:
- Pipeline:
- Steps:
- Output format:
- Ask before...
- Never...
- Stop when...
- Review checklist:
- Security checklist:
- Rollback:
- Edge cases:

------------------------------------------------------------

## 8. What To Reject

Reject:

- framework-specific rules that are not needed
- coding-only rules when the workspace is not coding-focused
- automatic commit or push behavior
- unsafe destructive behavior
- vague motivational text
- copied large external text
- secret-handling mistakes

------------------------------------------------------------

## 9. Promotion Rule

Promote only if the idea is:

- reusable
- safer than current behavior
- clear
- not too specific
- compatible with docs/data/automation work

------------------------------------------------------------

## 10. Git Rule

Before commit:

    git status
    git diff

Do not commit:

- secrets
- credentials
- auth files
- raw private source material
- backups
- exports
- databases

------------------------------------------------------------
