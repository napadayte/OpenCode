---
name: backup-restore
description: "Procedure for creating AND verifying backups, plus documenting the restore path. A backup without a verified restore is incomplete. Use for: WSL export, Docker volume, n8n data, databases, Conda envs. На русском: бэкап, восстановление, восстановить, n8n, докер вольюм. Українською: бекап, відновлення, відновити."
allowed-tools: Read, Glob, Grep, Edit, Write, Bash
risk: high
source: workspace
---

# Backup-Restore Skill

A reusable procedure for backing up sensitive workspace assets and **proving the restore works**.

## When to use

- before any destructive data change
- before migrating between machines
- on a scheduled basis for critical data
- when n8n data, Docker volumes, or databases are involved

## Inputs needed

- exact asset path (file / container / volume)
- target backup location (preferably outside the repo, e.g. external disk / OneDrive)
- expected size estimate
- restore environment (where you'd restore if disaster hits)

## Procedure

### 1. Identify the asset precisely

```bash
ls -lh <path>                        # file
docker volume inspect <volume>       # Docker volume
docker compose ps                    # services using the volume
```

For Docker / n8n: confirm exact volume name, mount point inside container, and which containers use it.

### 2. Plan the backup

Decide:
- backup format (tar.gz, sql dump, file copy, conda export, image export)
- destination path with date stamp: `<dest>/<asset>-YYYY-MM-DD_HH-MM.tar.gz`
- whether containers must stop (writes during backup → corrupt archive)

### 3. Create the backup

Standard patterns:

**File / folder:**
```bash
tar -czf "$DEST/$NAME-$(date +%F_%H-%M).tar.gz" -C "$(dirname "$SRC")" "$(basename "$SRC")"
```

**Docker volume:**
```bash
docker run --rm \
  -v <volume>:/data:ro \
  -v "$DEST":/backup \
  alpine tar -czf "/backup/<volume>-$(date +%F_%H-%M).tar.gz" -C /data .
```

**Postgres:**
```bash
docker compose exec -T <db-service> pg_dump -U <user> -d <db> | gzip > "$DEST/<db>-$(date +%F_%H-%M).sql.gz"
```

**SQLite:**
```bash
sqlite3 <db.sqlite> ".backup '$DEST/<db>-$(date +%F_%H-%M).sqlite'"
```

**Conda environment:**
```bash
conda env export --from-history -n <env> > "$DEST/conda-<env>-from-history.yml"
```

### 4. Verify the backup file

```bash
ls -lh "$DEST/<file>"                 # size sane?
tar -tzf "$DEST/<file>.tar.gz" | head # contents readable?
sha256sum "$DEST/<file>" > "$DEST/<file>.sha256"
```

### 5. Document restore command — and TEST it

Write the restore command into `docs/runbook.md` under a heading for this asset. Then run it against a throwaway target (different path, different volume, different DB name) to prove it works.

**A backup that has not been restored at least once is unverified.**

### 6. Update inventory

In `data/inventory.md`, set:
- `Backup method:` — the exact command above
- `Restore method:` — the exact command + verification check
- `Last verified:` — today's date

### 7. Schedule (if recurring)

If this asset needs recurring backups, document in `docs/runbook.md`:
- frequency
- retention policy (how many backups to keep)
- pruning command

## Restore procedure (when disaster strikes)

1. Confirm which backup file to restore (date, size, sha256).
2. Confirm the target environment is empty or backed up itself.
3. Run the documented restore command.
4. Verify by querying / listing contents.
5. Note in runbook: when restored, from which backup.

## Restrictions

- Never commit backup archives to git.
- Never store backups inside the repo (use `data/backups/` only as a documented local staging area, ignored by git).
- Never overwrite a working asset without first creating a fresh backup.
- For credentials embedded in backups: encrypt at rest, do not paste credential values into docs.
- Stop and ask if free disk is < 2× backup size.

## Output

- Backup file path + size + sha256
- Restore command (tested)
- Inventory entry updated
- Runbook entry added
