# 0001 Initial Workspace

------------------------------------------------------------

## Decision

Use an agent-ready workspace structure.

------------------------------------------------------------

## Context

This workspace is designed for:

- documentation
- research
- planning
- brainstorms
- automation notes
- n8n workflow documentation
- data inventory
- backup and recovery notes
- small helper tools
- lightweight scanners

It is not primarily a coding project.

------------------------------------------------------------

## Consequences

- agents share one contract through AGENTS.md
- detailed rules live in `.opencode/rules/`
- agent role definitions live in `.opencode/agents/`
- reusable procedures live in `.opencode/skills/`
- slash commands live in `.opencode/commands/`
- data is protected through data/inventory.md and .gitignore
- small code is allowed but controlled
- commits and pushes stay manual by default

------------------------------------------------------------
