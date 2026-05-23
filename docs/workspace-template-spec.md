# Agent-Ready Workspace Template Specification

------------------------------------------------------------

## 1. Purpose

This specification defines the `agent-ready-workspace` template.

This workspace is not primarily a coding project.

It is designed for:

- project thinking
- documentation
- research
- planning
- brainstorm sessions
- n8n automations
- data and database inventory
- backup and recovery notes
- operational procedures
- prompts
- checklists
- reports
- small helper scripts
- lightweight scanners and tools

Small code is allowed, but code is not the center of the workspace.

The workspace must support OpenCode, Codex CLI, Claude Code, and Gemini CLI through a shared project contract.

------------------------------------------------------------

## 2. Core Philosophy

The workspace must optimize for:

- clarity
- safety
- recoverability
- low chaos
- manual control
- agent interoperability
- long-term maintainability

Core rules:

- Classify first.
- Do not rush.
- Brainstorm before architecture.
- Plan before changes.
- Protect data.
- Protect secrets.
- Keep tasks small.
- Stop and re-plan on surprises.
- Review before commit.
- Commit manually.
- Push manually.
- Report every change.

This system should prevent lazy shortcuts, accidental data loss, secret leaks, and uncontrolled agent behavior.

------------------------------------------------------------

## 3. Workspace Structure

Target template name:

    agent-ready-workspace

Target path inside OpenCode config repo:

    projects/templates/agent-ready-workspace

Target user workspace command:

    new-agent-workspace <workspace-name>

Expected folder structure:

    agent-ready-workspace/
    ├── AGENTS.md
    ├── README.md
    ├── CLAUDE.md
    ├── GEMINI.md
    ├── opencode.json
    ├── docs/
    │   ├── overview.md
    │   ├── runbook.md
    │   ├── plans/
    │   │   └── README.md
    │   ├── reports/
    │   │   └── README.md
    │   └── decisions/
    │       └── 0001-initial-workspace.md
    ├── research/
    │   └── README.md
    ├── notes/
    │   └── README.md
    ├── prompts/
    │   └── README.md
    ├── checklists/
    │   └── README.md
    ├── automations/
    │   ├── README.md
    │   └── n8n/
    │       └── README.md
    ├── data/
    │   ├── README.md
    │   ├── inventory.md
    │   ├── schemas/
    │   │   └── README.md
    │   ├── exports/
    │   │   └── .gitkeep
    │   └── backups/
    │       └── .gitkeep
    ├── tools/
    │   ├── README.md
    │   ├── scripts/
    │   │   └── README.md
    │   └── scanners/
    │       └── README.md
    ├── .opencode/
    │   ├── instructions.md
    │   ├── agents/
    │   │   └── <slug>.md            (one per role)
    │   ├── skills/
    │   │   └── <slug>/SKILL.md      (one folder per skill)
    │   ├── commands/
    │   │   └── <slug>.md            (one per slash command)
    │   └── rules/
    │       ├── dispatch-policy.md
    │       ├── workflow.md
    │       ├── brainstorm.md
    │       ├── planning.md
    │       ├── document-style.md
    │       ├── git-operations.md
    │       ├── data-operations.md
    │       ├── automation-operations.md
    │       ├── light-code-policy.md
    │       └── security.md
    ├── .codex/
    │   └── config.toml
    ├── .claude/
    │   └── settings.json
    ├── .gemini/
    │   └── settings.json
    └── .gitignore

Main responsibilities:

- AGENTS.md is the shared contract for all agents.
- README.md is the human entry point.
- opencode.json holds OpenCode top-level permissions and defaults; agents and commands are file-based under `.opencode/`.
- docs/ contains operating documentation: overview, runbook, plans, reports, ADRs.
- .opencode/rules/ contains the real workflow system (read by every shell via the `instructions` array).
- .opencode/agents/ contains one `.md` per role; each file is a valid OpenCode agent definition.
- .opencode/skills/ contains reusable procedures, one `<slug>/SKILL.md` each (Anthropic Agent Skills spec).
- .opencode/commands/ contains slash command definitions, one `<slug>.md` each.
- research/ contains research notes and source summaries.
- notes/ contains informal notes.
- prompts/ contains reusable prompts.
- checklists/ contains repeatable checklists.
- automations/ contains automation designs and n8n notes.
- data/ contains inventory, schemas, and placeholders for local data areas.
- tools/ contains small helper scripts and scanners only.
- shell adapter folders configure OpenCode, Codex, Claude, and Gemini.

The workspace must remain document-first and operations-first.

The tools folder must not quietly grow into a large application without an explicit decision.

------------------------------------------------------------

## 4. Agent Roles

The workspace is organized around roles, not around one specific AI shell.

All shells should follow the same role logic.

### 4.1 Dispatcher

Classifies the request and chooses the workflow.

Responsibilities:

- identify task type
- decide if clarification is needed
- decide if brainstorm is needed
- decide if planning is needed
- decide which rule files apply
- avoid immediate file edits on non-trivial tasks

The dispatcher should not rush into execution.

### 4.2 Brainstormer

Generates options before a decision is made.

Responsibilities:

- propose multiple options
- compare tradeoffs
- identify assumptions
- identify unknowns
- identify risks
- recommend a practical direction

Brainstormer does not edit files.

### 4.3 Devil

Challenges plans and ideas.

Responsibilities:

- find weak assumptions
- find edge cases
- detect overengineering
- detect lazy shortcuts
- ask uncomfortable questions
- prevent bad architecture decisions

Devil is mandatory for important workspace, data, automation, backup, and financial decisions.

### 4.4 Planner

Turns a selected direction into an actionable plan.

Responsibilities:

- define goal
- list affected files
- break large work into smaller tasks
- define verification
- define rollback
- identify risks
- identify required approvals

Planner does not hide uncertainty.

### 4.5 Researcher

Collects and organizes information.

Responsibilities:

- summarize sources
- extract useful ideas
- separate facts from assumptions
- compare options
- cite sources when web research is used
- preserve useful references

Researcher should not turn research into action without planning.

### 4.6 Writer

Creates and updates documents.

Responsibilities:

- write clear Markdown
- keep structure consistent
- avoid vague filler
- avoid unnecessary theory
- update related docs when needed
- keep docs actionable

Writer should prefer useful operational clarity over beautiful but useless text.

### 4.7 Reviewer

Checks output quality.

Responsibilities:

- find contradictions
- find missing steps
- find unsafe assumptions
- check if the result matches the request
- check if files are in the right place
- check if risks are documented

Reviewer does not silently fix; reviewer reports.

### 4.8 Data Steward

Protects data, databases, exports, backups, and storage.

Responsibilities:

- maintain data inventory
- identify where data lives
- identify data sensitivity
- require backup plans before risky changes
- document restore paths
- prevent database dumps from entering git
- protect credentials and secrets

Data Steward is mandatory for database, Docker volume, n8n data, market data, exports, backups, and restore tasks.

### 4.9 Automation Operator

Handles workflow and automation work.

Responsibilities:

- design n8n workflows
- document triggers and actions
- map inputs and outputs
- document failure modes
- document retry and recovery behavior
- involve Data Steward when data is touched
- involve Security Reviewer when credentials are involved

Automation Operator should not create hidden fragile workflows.

### 4.10 Git Operator

Handles git safety and sync.

Responsibilities:

- inspect git status
- inspect git diff
- avoid accidental commits
- avoid accidental push
- avoid force push
- handle branch and sync logic
- document conflict resolution

Git Operator must keep user in manual control.

### 4.11 Recovery Operator

Handles backup and restore workflows.

Responsibilities:

- WSL export
- Docker volume backup
- n8n backup
- Conda environment export
- restore documentation
- disaster recovery checklist
- verification after backup

Recovery Operator must document how to restore, not only how to backup.

### 4.12 Light Coder

Writes small helper scripts only when needed.

Responsibilities:

- keep scripts small
- explain inputs and outputs
- avoid unnecessary frameworks
- avoid hidden dependencies
- include run instructions
- avoid secrets in code
- avoid turning workspace into a large codebase

Light Coder is allowed for tools, scanners, parsers, report generators, and automation helpers.

### 4.13 Security Reviewer

Checks secrets, permissions, exposure, and risky workflows.

Responsibilities:

- prevent secrets in git
- identify exposed credentials
- review auth/session files
- review financial/API risks
- review automation permissions
- review destructive commands
- review external data sharing

Security Reviewer is mandatory when credentials, APIs, financial data, broker tools, external integrations, or sensitive data are involved.

------------------------------------------------------------

## 5. Workflow Pipelines

Every non-trivial task must follow a workflow pipeline.

The goal is to prevent agents from rushing, guessing, touching risky files, or making broad changes without a plan.

### 5.1 Universal Entry Flow

For every task:

1. Classify the task.
2. Identify the environment.
3. Identify the affected area.
4. Check whether clarification is needed.
5. Check whether brainstorm is needed.
6. Check whether planning is needed.
7. Read the relevant rule files.
8. Proceed only within the approved scope.

Environment must be explicit when relevant:

- Windows
- WSL
- Docker
- Conda
- GitHub
- OneDrive
- Mac
- cloud service
- local database
- n8n

If the environment is unclear, stop and ask.

### 5.2 Mandatory Pipeline Triggers

A task must use a pipeline, not immediate execution, when it involves:

- more than 3 files
- data or databases
- backups
- restore operations
- Docker volumes
- n8n data
- credentials
- auth files
- session files
- financial data
- stock scanner logic
- GitHub sync
- Windows / WSL / Mac sync
- automation workflow changes
- agent rules
- project templates
- deleting files
- moving files
- installing tools
- changing global configs

### 5.3 Brainstorm Pipeline

Use for:

- new ideas
- architecture choices
- tool choices
- workspace design
- automation design
- database design
- financial scanner design
- unclear tasks
- strategic decisions

Pipeline:

1. Brainstormer proposes options.
2. Devil challenges the options.
3. Planner proposes a practical path.
4. User chooses direction.

Output must include:

- goal
- assumptions
- options
- pros and cons
- risks
- unknowns
- recommended option
- next steps
- decision needed from user

Brainstorm must not edit files.

Brainstorm must not run destructive commands.

Brainstorm must not commit or push.

### 5.4 Documentation Pipeline

Use for:

- README
- AGENTS.md
- SOP
- runbook
- checklist
- project documentation
- workflow documentation
- research summary
- decision records

Pipeline:

1. Planner defines scope.
2. Writer drafts or updates the document.
3. Reviewer checks clarity and consistency.
4. User approves or requests revision.

Output must include:

- changed files
- what changed
- why it changed
- how to verify
- remaining risks
- next recommended step

### 5.5 Workspace Setup Pipeline

Use for:

- new workspace
- folder structure
- template creation
- global instructions
- agent rules
- shell adapters
- project initialization

Pipeline:

1. Planner proposes structure.
2. Devil checks overengineering and missing parts.
3. Operator creates files only after approval.
4. Reviewer checks tree, files, and git status.
5. User commits manually unless commit was explicitly requested.

Workspace setup must be done carefully because templates spread mistakes to future projects.

### 5.6 Data / Database Pipeline

Use for:

- SQLite
- Postgres
- Supabase
- Docker volumes
- n8n data
- CSV exports
- market data
- schemas
- data backup
- data restore
- data migration
- data cleanup

Pipeline:

1. Data Steward identifies data location and risk.
2. Backup or rollback path is documented.
3. Planner defines the change.
4. Operator performs only the approved change.
5. Reviewer verifies the result.
6. Data inventory is updated.

No risky data operation should happen without a documented backup or rollback path.

### 5.7 Automation / n8n Pipeline

Use for:

- n8n workflow design
- workflow documentation
- trigger/action mapping
- API automation
- scheduled tasks
- integrations
- notification flows
- data movement

Pipeline:

1. Planner defines workflow goal.
2. Automation Operator maps trigger, actions, data flow, and errors.
3. Data Steward reviews if data is involved.
4. Security Reviewer reviews credentials and permissions.
5. Writer documents the workflow.
6. Reviewer checks the final result.

Required documentation:

- purpose
- trigger
- inputs
- outputs
- credentials involved
- data touched
- failure modes
- retry behavior
- manual recovery
- owner

### 5.8 Light Code Pipeline

Use for:

- small scripts
- data parsers
- stock scanner prototypes
- report generators
- automation helpers
- one-off tools

Pipeline:

1. Planner defines goal.
2. Light Coder writes minimal code.
3. Reviewer checks simplicity and correctness.
4. Security Reviewer checks secrets and API risks when relevant.
5. Data Steward checks data input and output when relevant.

Before code:

- define input
- define output
- define run command
- define dependencies
- define risk
- define verification

After code:

- show changed files
- show how to run
- show how to verify
- show known limitations

Light code must stay small unless the user explicitly decides to promote it into a separate coding project.

### 5.9 Backup / Recovery Pipeline

Use for:

- WSL export
- Docker volume backup
- n8n backup
- Conda environment export
- local database backup
- restore procedure
- disaster recovery

Pipeline:

1. Recovery Operator identifies what must be protected.
2. Data Steward identifies sensitive data.
3. Planner defines backup or restore steps.
4. Operator executes only approved commands.
5. Reviewer verifies backup artifact or restore result.
6. Runbook is updated.

Backup without restore instructions is incomplete.

### 5.10 Git Sync Pipeline

Use for:

- commit planning
- push
- pull
- branch sync
- conflict resolution
- GitHub repository setup
- Mac / Windows / WSL sync

Pipeline:

1. Git Operator checks current branch and status.
2. Reviewer checks unexpected changes.
3. Planner defines safe git action.
4. User approves commit or push.
5. Git Operator runs approved commands.
6. Final status is checked.

Manual commit and manual push are preferred.

### 5.11 Stop and Re-plan Rule

Stop immediately and re-plan when:

- command output is unexpected
- path is not what was expected
- git status shows unrelated changes
- conflict appears
- secret file appears
- data file appears unexpectedly
- command may delete data
- Windows and WSL paths are mixed
- Docker or volume operation is unclear
- backup is missing before risky operation
- agent is unsure

Do not keep pushing through uncertainty.

------------------------------------------------------------

## 6. Data / Database Rules

Data is a first-class part of the workspace.

Database and data operations must be handled more carefully than normal documents because mistakes can cause permanent loss, secret exposure, or corrupted automation.

### 6.1 Data Scope

The data layer includes:

- SQLite databases
- Postgres databases
- Supabase projects
- Docker volumes
- n8n data
- CSV files
- JSON exports
- market data
- generated reports
- local caches
- backup archives
- schemas
- credentials related to data access

### 6.2 Data Inventory

Every important data asset should be documented in:

    data/inventory.md

Each asset should include:

- name
- type
- location
- owner
- purpose
- contains secrets
- contains personal data
- contains financial data
- backup method
- restore method
- can commit to git
- notes

If an asset is not documented, treat it as risky.

### 6.3 Default Data Safety Rules

Default rules:

- do not delete data without explicit confirmation
- do not overwrite data without explicit confirmation
- do not modify a database without a backup or rollback plan
- do not commit database files
- do not commit database dumps
- do not commit exports containing private data
- do not commit credentials
- do not commit auth files
- do not commit broker or API keys
- document restore path before risky operations

### 6.4 Git Policy for Data

Usually safe to commit:

- schema documentation
- empty example files
- data dictionaries
- inventory documents
- sample data only when sanitized
- config.example files
- README files

Usually not safe to commit:

- real database files
- SQLite files
- database dumps
- private CSV exports
- large generated reports
- backup archives
- Docker volume exports
- n8n volume backups
- credentials
- tokens
- API keys
- OAuth files

### 6.5 Database Files

Never commit by default:

- *.sqlite
- *.sqlite3
- *.db
- *.db3
- *.dump
- *.sql
- *.backup
- *.bak

Exception requires explicit user approval and a clear reason.

Even then, data must be checked for secrets and private information first.

### 6.6 Exports and Backups

Folders such as these are local working areas:

    data/exports/
    data/backups/

They may exist in the workspace structure, but their contents should normally be ignored by git.

Use .gitkeep only to preserve folder structure.

Backup files should live in protected backup storage, not in normal project commits.

### 6.7 n8n Data

n8n data may include:

- workflows
- credentials references
- execution history
- binary data
- SQLite database
- local files
- logs

Treat n8n data as sensitive by default.

Before changing n8n data:

1. identify Docker volume or storage path
2. document backup command
3. create backup if needed
4. verify backup exists
5. only then proceed

### 6.8 Docker Volumes

Docker volumes are not normal folders.

Before touching a Docker volume:

- list volumes
- identify target volume
- inspect related containers
- stop container if needed
- backup volume
- verify backup archive
- document restore command

Never delete a Docker volume unless explicitly confirmed.

### 6.9 Market Data and Stock Scanner Data

Market and stock scanner data must be treated as research data.

Required documentation:

- data source
- collection method
- update frequency
- assumptions
- limitations
- storage location
- whether data can be redistributed
- whether API credentials are involved

The workspace may produce research or analytics signals.

The workspace must not execute trades by default.

The workspace must not present scanner output as financial advice.

### 6.10 Recovery Requirement

For important data, backup is not enough.

The workspace must document:

- how to create backup
- where backup is stored
- how to restore
- how to verify restore
- what can go wrong
- who approves destructive restore operations

A backup that has no restore path is incomplete.

### 6.11 Data Steward Trigger

Data Steward must be involved when the task mentions:

- database
- data
- storage
- backup
- restore
- Docker volume
- n8n data
- SQLite
- Postgres
- Supabase
- CSV export
- market data
- scanner data
- credentials for data access

When in doubt, involve Data Steward.

------------------------------------------------------------

## 7. Light Code Rules

This workspace may contain small code, but it is not primarily a software application.

Light code is allowed when it supports the workspace.

Examples:

- small Python scripts
- data parsers
- report generators
- stock scanner prototypes
- automation helpers
- n8n helper scripts
- one-off conversion tools
- small CLI utilities
- small analysis notebooks only when needed

Light code must stay small, explicit, and understandable.

### 7.1 When Code Is Allowed

Code is allowed when the goal is:

- automate a repeated manual task
- analyze data
- generate a report
- transform files
- prototype a scanner
- support n8n workflows
- validate an idea
- create a small internal tool

Code is not allowed to silently become the center of the workspace.

If the tool grows into a real application, it should be promoted to a separate project.

### 7.2 Before Writing Code

Before writing code, define:

- goal
- input
- output
- run command
- dependencies
- expected files touched
- risks
- verification method
- rollback method

If these are unclear, ask first.

### 7.3 Code Location

Small scripts should live in:

    tools/scripts/

Scanner prototypes should live in:

    tools/scanners/

Automation helpers should live in:

    automations/

Project-specific notes should be documented next to the tool.

Every non-trivial tool should include a README or notes file.

### 7.4 Dependency Rules

Prefer standard library first.

Avoid new dependencies unless they clearly reduce risk or complexity.

If adding a dependency, document:

- package name
- why needed
- install command
- where it is used
- risk
- uninstall or rollback notes

Do not install global tools without explicit approval.

### 7.5 Python Rules

Python scripts should:

- be readable
- use clear names
- handle missing files
- avoid hardcoded personal paths when possible
- avoid hardcoded secrets
- print useful errors
- include a simple run command
- keep configuration separate from code

Use config.example files for examples.

Use local config files for private values.

Local config files must be ignored by git.

### 7.6 Financial Scanner Rules

For stock scanner or market-data code:

Allowed:

- screening
- research
- analytics
- watchlists
- backtesting notes
- report generation
- educational calculations

Not allowed by default:

- automatic trading
- order execution
- broker account actions
- storing broker credentials in repo
- presenting output as financial advice

Required:

- data source documented
- assumptions documented
- limitations documented
- no secret keys in git
- clear separation between signal and trade execution
- manual review before real-world action

Standard disclaimer:

This workspace may produce research or analytics signals. It does not execute trades and does not provide financial advice.

### 7.7 Secrets in Code

Never hardcode:

- API keys
- broker credentials
- OAuth tokens
- passwords
- cookies
- private keys
- account IDs when sensitive
- personal access tokens

Use local ignored config files or environment variables.

Example files must use fake placeholder values only.

### 7.8 Generated Outputs

Generated outputs should not be committed by default.

Usually ignore:

- reports generated from private data
- CSV exports
- database files
- cache files
- logs
- temporary files
- large artifacts

Commit only sanitized examples or documentation.

### 7.9 Testing Light Code

Testing does not need to be heavy.

Minimum verification:

- run the script
- verify expected output
- verify no unexpected files changed
- verify errors are understandable
- verify secrets are not printed
- verify git status

For data tools, also verify:

- input file path
- output file path
- row counts if relevant
- sample output
- failure behavior when input is missing

### 7.10 Promotion Rule

If a light tool needs:

- many modules
- a package manager
- a database
- a web UI
- multiple users
- deployment
- tests
- CI/CD
- long-term maintenance

then it should be promoted into a separate project.

The workspace may document the project, but should not become an accidental software monolith.

------------------------------------------------------------

## 8. Security Rules

Security is a default requirement.

The workspace may contain documentation, automation notes, data inventory, scripts, and integration plans. Any of these can accidentally expose secrets or sensitive data.

### 8.1 Never Commit

Never commit:

- .env
- .env.*
- auth files
- tokens
- credentials
- API keys
- private keys
- OAuth files
- session files
- cookies
- database dumps
- personal data exports
- broker credentials
- cloud credentials
- password manager exports
- production config
- real customer data
- real private financial data

### 8.2 Sensitive Local Paths

Treat these paths as sensitive:

- ~/.codex/auth.json
- ~/.codex/history.jsonl
- ~/.codex/*.sqlite
- ~/.claude.json
- ~/.claude/
- ~/.gemini/oauth_creds.json
- ~/.gemini/google_accounts.json
- ~/.gemini/history/
- ~/.gemini/tmp/
- Docker volumes
- n8n volume data
- local database files
- backup archives
- browser profile data
- SSH keys
- cloud CLI credentials

Do not print their contents.

Do not copy them into project repos.

Do not upload them unless explicitly required and safe.

### 8.3 Secret Detection

Before committing, check for:

- API keys
- tokens
- passwords
- private keys
- bearer tokens
- database URLs
- OAuth credentials
- broker credentials
- email credentials
- webhook URLs
- personal access tokens

If a secret is found, stop.

Do not commit.

Ask the user before cleanup.

### 8.4 External Services

Extra care is required when working with:

- GitHub
- OpenAI
- Anthropic
- Google
- n8n
- Docker
- Supabase
- cloud providers
- broker APIs
- financial data APIs
- email services
- webhooks

For each integration, document:

- service name
- purpose
- credentials involved
- data sent
- data received
- failure mode
- revoke method
- owner

### 8.5 Automation Security

Automation can leak data faster than manual work.

For n8n or automation tasks, document:

- trigger
- credentials used
- data touched
- destination services
- logs produced
- retry behavior
- failure behavior
- manual stop procedure

Do not create automations that send private data externally without explicit approval.

### 8.6 Financial Security

For market data, stock scanner, or broker-related work:

- do not store broker credentials in git
- do not print tokens
- do not execute trades by default
- do not connect trading actions without explicit separate approval
- do not present signals as financial advice
- document data sources
- document assumptions
- document limitations

Financial tooling must stay research-only unless the user explicitly creates a separate approved trading system.

### 8.7 Database Security

Database-related tasks must protect:

- connection strings
- passwords
- tokens
- dumps
- private records
- personal data
- execution logs
- backups

Before sharing or committing database-related files, check whether they contain secrets or private data.

### 8.8 Backup Security

Backups may contain everything.

Treat backups as sensitive by default.

Do not commit:

- WSL exports
- Docker volume backups
- n8n_data backups
- database backups
- Conda full exports if they contain private paths or tokens
- full archive dumps

Backup storage should be separate from normal git repositories.

### 8.9 Security Reviewer Trigger

Security Reviewer must be involved when:

- credentials are mentioned
- auth files are touched
- APIs are connected
- automation sends data externally
- financial tools are involved
- broker tools are involved
- user data is exported
- database dumps are created
- public sharing is requested
- permissions are changed
- destructive commands are proposed

When in doubt, involve Security Reviewer.

### 8.10 Incident Rule

If a secret may have been exposed:

1. Stop.
2. Do not commit.
3. Do not push.
4. Identify what was exposed.
5. Remove it from working files.
6. Rotate or revoke the secret if needed.
7. Check git history if it was committed.
8. Document what happened.
9. Ask the user before further action.

------------------------------------------------------------

## 9. Git Rules

Git is used for history, rollback, sync, review, and safe experimentation.

Git is not only for code.

In this workspace, Git protects:

- documentation
- plans
- prompts
- checklists
- architecture decisions
- automation notes
- data inventory
- small scripts
- project structure

### 9.1 Default Git Rules

Default rules:

- inspect git status before changes
- inspect git diff after changes
- do not commit unless explicitly requested
- do not push unless explicitly requested
- keep commits small
- commit related changes together
- do not mix unrelated work in one commit
- never force push without explicit confirmation
- never commit secrets
- never commit generated backups
- never commit database dumps
- never commit local auth/session files
- never commit large private exports

Manual commit and manual push are preferred.

### 9.2 Before Any Change

Before modifying files, check:

    git status

If there are unexpected changes, stop and ask.

Unexpected changes include:

- files modified by another tool
- files outside the requested scope
- untracked secrets
- database files
- backup archives
- generated exports
- auth files
- merge conflicts

Do not continue through an unclear git state.

### 9.3 After Any Change

After modifying files, check:

    git status
    git diff

Final report must include:

- changed files
- summary of changes
- verification performed
- risks
- next recommended step

If a file was created, explain why it belongs there.

If a file was deleted, explain why deletion was safe.

### 9.4 Commit Policy

Do not commit automatically.

Commit only when the user explicitly asks.

Before commit:

1. Show git status.
2. Show diff summary.
3. Confirm no secrets are included.
4. Confirm no generated private data is included.
5. Confirm commit message.

Preferred commit style:

    Add workspace template specification
    Add data operations rules
    Update n8n workflow notes
    Document backup procedure

Avoid vague commit messages:

    update
    fix
    stuff
    changes
    work

### 9.5 Push Policy

Do not push automatically.

Push only when the user explicitly asks.

Before push:

1. Confirm current branch.
2. Confirm remote.
3. Confirm local commits.
4. Confirm no secrets.
5. Confirm the user wants to publish.

Check:

    git branch --show-current
    git remote -v
    git log --oneline --max-count=5
    git status

### 9.6 Branch Policy

Use simple branch names.

Examples:

    main
    docs/workspace-template
    backup/n8n-notes
    automation/n8n-cleanup
    data/inventory-update

Avoid unclear branch names:

    temp
    test
    new
    final
    final2

For normal solo workspace use, `main` is acceptable.

For risky work, create a branch first.

### 9.7 Sync Policy

When syncing between Windows, WSL, Mac, and GitHub:

- GitHub is the source of truth for committed workspace files.
- Local auth files are not synced through Git.
- Large backups are not synced through Git.
- Data exports are not synced through Git unless explicitly sanitized.
- Each machine should clone the repo and recreate local secrets separately.

Before pulling:

    git status

If local changes exist, decide:

- commit
- stash
- discard
- copy elsewhere
- stop and ask

Do not pull into a dirty repo unless the user understands the risk.

### 9.8 Conflict Policy

If a merge conflict appears:

1. Stop.
2. Show conflicted files.
3. Explain what happened.
4. Do not guess blindly.
5. Resolve one file at a time.
6. Show final diff.
7. Ask before commit.

Commands to inspect:

    git status
    git diff
    git diff --name-only --diff-filter=U

### 9.9 Files That Should Not Enter Git

Never commit:

- .env
- .env.*
- auth.json
- tokens
- credentials
- API keys
- private keys
- OAuth files
- session files
- cookies
- database files
- database dumps
- backup archives
- Docker volume exports
- n8n data backups
- WSL exports
- private CSV exports
- personal data exports
- broker credentials
- local config files with secrets

### 9.10 Gitignore Requirements

The workspace .gitignore must block:

- secrets
- environment files
- local config files
- auth files
- database files
- database dumps
- exports
- backups
- logs
- caches
- node_modules
- Python virtual environments
- archives
- OS/editor noise

It should keep important folder structure using `.gitkeep` when needed.

### 9.11 Recovery Through Git

Git can restore committed files.

Useful commands:

    git status
    git diff
    git log --oneline
    git show <commit>
    git restore <file>

Do not use destructive git commands without explicit approval.

Dangerous commands:

    git reset --hard
    git clean -fd
    git push --force
    git checkout -- .
    git restore .

These require explicit confirmation and explanation.

### 9.12 Git Operator Trigger

Git Operator must be involved when the task mentions:

- commit
- push
- pull
- branch
- merge
- conflict
- sync
- GitHub
- rollback
- restore file
- reset
- clean
- force push
- Mac sync
- Windows sync
- WSL sync

When in doubt, inspect status first.

------------------------------------------------------------

## 10. Success Criteria

The `agent-ready-workspace` template is successful only if it is useful in daily work and safe under pressure.

### 10.1 Template Success

The finished template must provide:

- clear workspace structure
- clear agent contract
- clear workflow rules
- brainstorm workflow
- data/database rules
- backup/recovery rules
- automation/n8n rules
- light-code lane
- git safety
- security rules
- shell adapters
- human-readable README
- operational runbook

A new workspace must be understandable without asking the original creator.

### 10.2 Tool Compatibility

The workspace must work with:

- OpenCode
- Codex CLI
- Claude Code
- Gemini CLI

Each shell must be able to:

- read AGENTS.md
- find the relevant rule files
- understand that this is not primarily a codebase
- analyze without editing
- plan before changes
- protect data and secrets
- summarize work clearly

### 10.3 Creation Success

A new workspace must be creatable with:

    new-agent-workspace <workspace-name>

The command must:

- copy the template
- update README title
- initialize git
- use main branch
- avoid copying node_modules
- avoid copying caches
- avoid copying auth files
- avoid copying generated data
- preserve folder structure
- print next steps

### 10.4 Safety Success

The template must prevent common failures:

- accidental secret commit
- accidental database commit
- accidental backup archive commit
- accidental Docker volume deletion
- accidental n8n data loss
- accidental force push
- accidental mixing of Windows and WSL paths
- uncontrolled agent edits
- lazy undocumented changes
- large unclear tasks

### 10.5 Data Success

Data handling is successful when:

- important data assets are listed in data/inventory.md
- backups have restore instructions
- exports are ignored by git
- backups are ignored by git
- database files are ignored by git
- credentials are never stored in repo
- n8n data is treated as sensitive
- market data sources are documented
- financial scanner limitations are documented

### 10.6 Light Code Success

Light code handling is successful when:

- scripts stay small
- scripts have clear purpose
- inputs are documented
- outputs are documented
- run commands are documented
- dependencies are documented
- secrets are not hardcoded
- generated outputs are ignored
- tools do not become accidental large applications

### 10.7 Documentation Success

Documentation is successful when it answers:

- what is this workspace for
- what is active now
- where important files live
- how to run routine operations
- how to recover from common failures
- what data exists
- what should not be committed
- which workflow to use
- what the next step is

Documentation should be useful, not decorative.

### 10.8 Agent Behavior Success

Agent behavior is successful when agents:

- classify first
- ask when unclear
- brainstorm before architecture
- plan before risky changes
- split large tasks
- protect secrets
- protect data
- stop on surprises
- report changed files
- report verification
- report risks
- do not commit unless asked
- do not push unless asked

### 10.9 Demo Verification

Before using the template for real work, verify it with a demo workspace:

    ~/code/demo-agent-workspace

Verification must include:

- create workspace with new-agent-workspace
- inspect tree
- check git status
- run OpenCode analyze
- run Codex analyze
- run Claude analyze
- run Gemini analyze
- confirm no files were unexpectedly changed
- confirm shell adapters are readable
- confirm rules are discoverable

### 10.10 Final Acceptance

The workspace system is accepted when:

- specification is committed
- template is committed
- new-agent-workspace command is committed
- demo workspace passes verification
- OpenCode repo is clean
- GitHub sync works
- no secrets are committed
- daily usage is simple enough to remember

If the system feels clever but hard to use, it is not finished.

The final system should feel boring, predictable, safe, and easy to continue.

------------------------------------------------------------
