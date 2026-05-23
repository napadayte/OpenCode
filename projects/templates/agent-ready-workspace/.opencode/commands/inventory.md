---
description: Update data/inventory.md with a new or changed asset
agent: data-operator
---

Asset: $ARGUMENTS

Use the `data-operator` agent and `data-inventory` skill from `.opencode/skills/data-inventory/SKILL.md`.

Procedure:

1. Read `data/inventory.md` — confirm whether this asset is already listed.
2. Read `.opencode/rules/data-operations.md`, `.opencode/rules/security.md`.
3. Identify the asset: path / container / volume, type, source, sensitivity.
4. Identify backup method and restore method. If restore has never been verified, mark as `Last verified: not verified`.
5. Add or update the entry using the template in `data/inventory.md`.
6. Cross-check `.gitignore` — make sure sensitive paths are excluded.

Output:

- Inventory entry created / updated (path + summary)
- Sensitivity level
- Backup method + restore method
- `.gitignore` checked / updated
- Next recommended step (e.g., verify restore)

Restrictions:

- Never paste real credentials, real connection strings with passwords, or real personal data.
- Never mark an asset as backed-up unless a restore has been verified at least once.
- Do not commit unless explicitly asked.
