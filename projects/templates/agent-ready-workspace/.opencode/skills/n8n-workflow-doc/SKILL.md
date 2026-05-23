---
name: n8n-workflow-doc
description: "Procedure for documenting an n8n workflow: trigger, actions, inputs, outputs, credentials, failure modes, recovery. Use whenever an n8n workflow is created, modified, or audited. На русском: задокументировать n8n воркфлоу, описать автоматизацию, триггер, действия. Українською: задокументувати n8n воркфлоу."
---

# n8n Workflow Doc Skill

A reusable procedure for producing reliable documentation of an n8n workflow.

## When to use

- a new n8n workflow is created
- an existing workflow is modified
- auditing an inherited workflow before changes
- before exporting / sharing a workflow

## Inputs needed

- workflow name (matches n8n UI exactly)
- workflow ID (from URL)
- environment (local docker / cloud / hosted)
- access to the n8n UI

## Procedure

### 1. Create the doc file

`automations/n8n/<workflow-name>.md`

### 2. Fill these sections (in this order)

```markdown
# <Workflow Name>

## Purpose
One sentence: what business outcome this produces.

## Owner
Who maintains this.

## Status
draft | active | paused | deprecated

## Trigger
- Type: webhook | schedule | manual | event
- Details: cron / URL / event name
- Authentication: which credential, if any

## Inputs
- Source: where data comes from
- Shape: example payload (sanitized — no real data)
- Validation: what's checked before downstream nodes

## Actions (node sequence)
1. <Node type> — <what it does>
2. <Node type> — <what it does>
3. ...

## Outputs
- Destination: where data goes (service, channel, file)
- Format: shape of the output
- Side effects: emails sent, rows written, alerts triggered

## Credentials involved
- <credential-name-in-n8n>: <service> (NEVER write the secret itself)

## Data touched
- <asset>: read | write | delete
- Involve `data-operator` if real data is touched

## Failure modes
- <what can fail>: <how it manifests>

## Retry & recovery
- Built-in retries: yes/no, count, backoff
- Manual recovery: <exact steps to recover from each failure mode>

## Manual stop procedure
- How to disable safely (UI / API / docker)

## Verification
- How to test end-to-end without affecting production data
- Sample input → sample output

## Change log
- YYYY-MM-DD: <change>
```

### 3. Sanitize the exported JSON

Never commit raw n8n exports with credentials embedded. If exporting:
- export to `automations/n8n/<workflow-name>.json`
- strip credential IDs / values before commit
- add to `.gitignore` if uncertain

### 4. Cross-link

- Add link from `automations/README.md` index
- Reference in `data/inventory.md` if the workflow touches data assets

### 5. Verify before declaring done

- Read the doc; can someone unfamiliar reproduce or stop the workflow from this alone?
- Are all credentials referenced by name (not value)?
- Is at least one failure mode documented?

## Restrictions

- Never paste credential values, tokens, webhook secrets, or API keys into the doc.
- Never document a workflow as "active" unless verification was performed.
- Never auto-run a workflow as part of documentation.

## Output

- Doc path
- Trigger and destination summary
- Number of failure modes documented
- Credentials list (names only)
- Verification status
