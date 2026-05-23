---
name: security-check
description: "Read-only secret-and-risk audit of pending changes or any specified file/folder. Scans for credentials, dangerous commands, and exposure paths. На русском: проверь на секреты, проверка безопасности, утечки, опасные команды. Українською: перевір на секрети, перевірка безпеки, витоки."
---

# Security Check Skill

A reusable read-only audit procedure. Use **before** any commit / push / share.

## When to use

- before `git commit`
- before `git push`
- before sharing a workspace export or backup
- before merging a PR
- before enabling an n8n workflow that touches external services
- when credentials, APIs, financial tools, or external integrations are mentioned

## Scope

The audit covers:
1. secret patterns in files
2. dangerous commands in scripts
3. unsafe gitignore configuration
4. exposed local config files

## Procedure

### 1. Determine the scope of the audit

- For a commit audit: `git diff --cached --name-only`
- For a folder audit: list files via `Glob`
- For a workflow audit: target `automations/n8n/`, `tools/scripts/`

### 2. Secret patterns

Search for (case-insensitive):

```
password\s*[:=]
secret\s*[:=]
api[_-]?key\s*[:=]
token\s*[:=]
bearer\s+[A-Za-z0-9._\-]+
authorization\s*:
client[_-]?secret\s*[:=]
aws[_-]?(access|secret)
openai[_-]?api[_-]?key
anthropic[_-]?api[_-]?key
private[_-]?key
BEGIN\s+(RSA|EC|DSA|OPENSSH|PRIVATE)\s+KEY
postgres://[^/\s]*:[^@\s]*@
mysql://[^/\s]*:[^@\s]*@
mongodb(\+srv)?://[^/\s]*:[^@\s]*@
https://hooks\.slack\.com/services/
https://discord\.com/api/webhooks/
```

For each hit:
- file path + line number
- pattern matched (NOT the value)
- proposed action (move to env, ignore file, rotate if already committed)

### 3. Dangerous commands

Look for in scripts and automations:
- `rm -rf`, `rmdir /S`, `Remove-Item -Recurse -Force`
- `git push --force`, `git reset --hard`, `git clean -fd`
- `DROP DATABASE`, `TRUNCATE`, `DELETE FROM` without `WHERE`
- `docker volume rm`, `docker system prune -a`
- `chmod 777`, `chown -R`
- `curl ... | bash`, `wget ... | sh`

For each: file, line, what it does, safer alternative.

### 4. Gitignore audit

Check `.gitignore` blocks:
- `.env`, `.env.*`
- `auth.json`, `tokens`, `credentials`, `*.key`, `*.pem`
- `*.sqlite`, `*.db`, `*.dump`, `*.sql`, `*.backup`
- archives: `*.tar`, `*.tar.gz`, `*.zip`
- `node_modules`, `__pycache__`, `.venv`
- caches: `.cache/`, `tmp/`, `logs/`

If missing patterns, propose additions.

### 5. Local config exposure

Scan for committed files matching:
- `config.local.*`
- `*.local.json`, `*.local.toml`
- files with literal `localhost:5432` + password
- files referencing personal paths (`/home/<user>`, `/Users/<user>`)

### 6. Report

```
Security check: <scope>

Critical:
  <findings that must block commit/push>

Important:
  <findings that need fixing>

Suggestions:
  <hardening recommendations>

Approval: APPROVE | REQUEST CHANGES | BLOCK
```

## Incident response

If a secret is found in already-committed history:
1. STOP. Do not push.
2. Treat the secret as compromised.
3. Rotate at the source (regenerate API key, revoke token).
4. Remove from working tree.
5. Ask user before rewriting git history.

## Restrictions

- Never print actual secret values — only patterns and locations.
- Never auto-fix — report only.
- Never push, even after a clean check.
- Never auto-rotate credentials.
