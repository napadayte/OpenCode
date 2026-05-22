---
name: stock-scanner-research
description: "Research-only stock scanner / market data work: screening, watchlists, signal analysis, report generation. NEVER executes trades. Documents sources, assumptions, limitations. На русском: сканер акций, исследование рынка, скринер, сигналы, ватчлист. Українською: сканер акцій, дослідження ринку, скринер."
allowed-tools: Read, Glob, Grep, Edit, Write, Bash
risk: high
source: workspace
---

# Stock Scanner Research Skill

A reusable procedure for building or extending market-data tooling in the workspace.

**Hard scope:** research only. Never executes trades. Never connects to broker accounts for orders.

## When to use

- prototyping a stock screener
- generating a watchlist from a data source
- documenting a backtesting idea
- building a report from market data
- documenting data sources and assumptions

## When NOT to use

- placing real orders
- automatic trading
- broker account actions
- presenting output as financial advice

Those require a separate, explicitly-approved project — not this workspace.

## Inputs needed

Before any code or data work:

- Data source(s): exact name, URL, API
- Access method: free / paid / API key / scraping
- License: redistribution rules, attribution requirements
- Data frequency: real-time / intraday / EOD / weekly
- Coverage: market, instrument types, history depth
- Storage: where data lives, sensitivity
- Goal: what question the scanner answers
- Output: report / CSV / dashboard / alert

## Procedure

### 1. Document the source

In `data/inventory.md`, add the data source as an asset with:
- name, path, type
- source URL
- license / redistribution
- sensitivity
- backup policy

In `automations/n8n/` or `tools/scanners/<name>/README.md`, add:
- API endpoint(s)
- rate limits
- error behavior

### 2. Document assumptions explicitly

Create `tools/scanners/<name>/assumptions.md` covering:
- universe (which tickers, how filtered)
- time zone of timestamps
- handling of corporate actions (splits, dividends)
- handling of missing data
- survivorship bias assumptions
- look-ahead bias assumptions
- transaction-cost model (if any backtesting)
- slippage model (if any backtesting)

### 3. Document limitations

`tools/scanners/<name>/limitations.md`:
- known sources of bias
- what the scanner does NOT model
- known failure modes
- universe blind spots

### 4. Implement using light-code-script skill

Follow `@.claude/skills/light-code-script/SKILL.md`.

Constraints specific to scanners:
- Never hardcode API keys → env vars only
- Always cache responses to avoid hammering the source
- Log raw responses to ignored local folder for debugging
- Provide a `--dry-run` mode that runs without external calls

### 5. Output as research artifact, not advice

Every scanner report MUST include a header:

```
This output is research-only and is not financial advice.
Data source: <name>. As of: <timestamp>.
Universe: <description>. Assumptions: <link to assumptions.md>.
Limitations: <link to limitations.md>.
```

### 6. Separate signal from execution

A signal file is a CSV / JSON / markdown report — never a broker API call. Implementing actual trades, even via webhook, requires a separate approved project.

### 7. Manual review before any real-world action

If the user wants to act on a signal:
- Show the user the report.
- Surface assumptions and limitations.
- Require explicit user confirmation per action.
- Log the decision.

## Restrictions

- Never store broker credentials in the repo.
- Never call broker order endpoints.
- Never present output as financial advice.
- Never claim backtest = future performance.
- Never auto-execute on a signal.
- Document data freshness — stale data is a major source of error.

## Output

- Scanner location (`tools/scanners/<name>/`)
- Data source(s) inventoried
- Assumptions and limitations documented
- Run command (with `--dry-run`)
- Verification (small sample produced expected shape)
- Disclaimer included in output
