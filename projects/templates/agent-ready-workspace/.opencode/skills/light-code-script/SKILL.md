---
name: light-code-script
description: "Write small Python or Bash script: parsers, report generators, scanner prototypes, automation helpers. Stdlib first, no hidden deps, no secrets in code. На русском: написать маленький скрипт, парсер, утилита. Українською: написати маленький скрипт, парсер."
allowed-tools: Read, Glob, Grep, Edit, Write, Bash
risk: medium
source: workspace
---

# Light Code Script Skill

A reusable procedure for producing small, maintainable helper scripts that support the workspace.

## When to use

- automating a repeated manual task
- transforming data files
- generating a report from existing data
- prototyping a scanner or analyzer
- supporting an n8n workflow

## When NOT to use

- multi-module application
- anything needing a database
- anything needing a web UI
- anything needing deployment / CI
- anything with long-term maintenance burden

→ Those go into a separate project, not this workspace.

## Inputs needed

Define **before writing any code**:

- Goal (one sentence)
- Language (Python / Bash; default Python for parsing, Bash for orchestration)
- Input: path, format, expected size
- Output: path, format
- Run command (full)
- Dependencies (prefer stdlib)
- Risks (what can break)
- Verification (how to know it worked)

If any input is unclear, ask first.

## Procedure

### 1. Choose location

- `tools/scripts/<name>.py` or `<name>.sh` — small standalone helpers
- `tools/scanners/<name>/` — scanner prototypes (own folder with README)
- `automations/<name>/` — automation helpers tightly coupled to an n8n workflow

### 2. Write minimal skeleton (Python)

```python
#!/usr/bin/env python3
"""<one-line purpose>

Run:
    python3 <path> <input> <output>
"""
import sys
import argparse
from pathlib import Path


def main(args: argparse.Namespace) -> int:
    src = Path(args.input)
    if not src.is_file():
        print(f"input not found: {src}", file=sys.stderr)
        return 1
    # ... real work
    return 0


def parse_args() -> argparse.Namespace:
    p = argparse.ArgumentParser(description=__doc__)
    p.add_argument("input")
    p.add_argument("output")
    return p.parse_args()


if __name__ == "__main__":
    sys.exit(main(parse_args()))
```

### 2b. Write minimal skeleton (Bash)

```bash
#!/usr/bin/env bash
set -euo pipefail

# <one-line purpose>
# Usage: <script> <input> <output>

if [ $# -lt 2 ]; then
  echo "Usage: $0 <input> <output>" >&2
  exit 1
fi

INPUT="$1"
OUTPUT="$2"

[ -f "$INPUT" ] || { echo "input not found: $INPUT" >&2; exit 1; }

# ... real work
```

### 3. Implement only what's needed

Stdlib first. No new dependency without:
- documenting package + version + why
- install command in script header or README
- where it's used

For Python: prefer `csv`, `json`, `pathlib`, `argparse`, `urllib.request` (no `requests` unless justified).

### 4. Handle errors explicitly

- Print useful errors to stderr.
- Use non-zero exit codes for failure.
- Detect missing inputs early.
- Never crash with bare traceback on user-facing errors.

### 5. Keep config separate

- Hardcoded values → top of file or `config.example.json`.
- Personal values → `config.local.json` (add to `.gitignore`).
- Secrets → environment variables only.

### 6. Add a sibling README for non-trivial tools

`tools/scripts/<name>.md` with:
- purpose
- run command
- example input + expected output
- known limitations
- dependencies

### 7. Verify

- Run on a small sample input.
- Confirm output is correct.
- Confirm no unexpected files created.
- Confirm git status is clean of stray output files.

## Restrictions

- No hardcoded secrets, API keys, tokens.
- No hardcoded personal paths (`/home/<user>/...`).
- No `curl ... | bash` patterns.
- No silent overwrite of existing output files (use `--force` flag if needed).
- No new dependency for one-line problems.
- Generated outputs go to `.gitignore` by default.

## Output

- Script path
- Run command (tested)
- Verification command
- Known limitations
- Sibling README (if non-trivial)
