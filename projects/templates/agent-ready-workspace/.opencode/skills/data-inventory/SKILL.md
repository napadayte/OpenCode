---
name: data-inventory
description: "Procedure for adding, updating, or removing entries in data/inventory.md. Used whenever a data asset is created, moved, deleted, or its sensitivity changes. На русском: инвентаризация данных, обновить инвентарь, добавить актив. Українською: інвентаризація даних, оновити інвентар."
---

# Data Inventory Skill

A reusable procedure for keeping `data/inventory.md` accurate.

## When to use

- a new data asset is added (database, export, CSV, backup, schema)
- an existing asset moves or is renamed
- an asset is deleted
- sensitivity changes (e.g. now contains personal data)
- backup or restore procedure changes
- before any task referencing data

## Inputs needed

For each asset:
- name
- path (or container / volume name)
- type (sqlite / postgres / csv / json / docker volume / n8n / archive)
- source (where it came from)
- owner (who maintains)
- sensitivity (public / personal / financial / credentials)
- git policy (commit / ignore)
- backup method
- restore method
- last verified date

## Procedure

### 1. Open the inventory

`data/inventory.md`. Skim existing entries to avoid duplicates.

### 2. Add or update entry

Use the standard template:

```
### <Asset Name>

Path: <full path or container:volume>
Type: <type>
Source: <where from>
Owner: <person / role>
Sensitivity: <public | personal | financial | credentials>
Git policy: <commit | ignore>
Backup method: <how to create>
Restore method: <how to restore + verify>
Last verified: <YYYY-MM-DD>
Notes: <anything important>
```

### 3. Cross-check `.gitignore`

If the asset has `Git policy: ignore`, confirm the path is matched by `.gitignore`. Add a pattern if missing.

### 4. For sensitive assets, also check

- Are credentials needed to access it? Where are they stored? (Never in git.)
- Is backup verified? When was the last successful restore test?
- Is there a manual stop / kill path?

### 5. For removed assets

Do not delete the entry. Instead:
- Append a `Removed: <YYYY-MM-DD>` field
- Add a `Removal note:` explaining why
- Keep the entry for audit history

### 6. If you find an undocumented asset

Treat it as risky:
- pause current task
- document it before proceeding
- involve `data-operator` and possibly `security-reviewer`

## Output

- Inventory entry created or updated (path + summary)
- `.gitignore` checked / updated
- Sensitivity confirmed
- Backup + restore documented
- Next recommended step

## Restrictions

- Never paste real credentials, real database connection strings with passwords, or real personal data into inventory.
- Use placeholders: `<owner>`, `<credential-name>`, `<region>`.
- Never mark an asset as backed-up unless a restore has been verified at least once.
