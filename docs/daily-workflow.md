# Daily Agent Workflow

------------------------------------------------------------

## 1. Main folders

Projects:

    ~/code

OpenCode config:

    ~/.config/opencode

Project template:

    ~/.config/opencode/projects/templates/agent-ready-project

Project creation command:

    new-agent-project <project-name>

------------------------------------------------------------

## 2. Create a new project

    cd ~/code
    new-agent-project my-project
    cd my-project

Then edit:

    README.md
    AGENTS.md
    docs/architecture.md
    docs/runbook.md

Start with OpenCode:

    opencode

------------------------------------------------------------

## 3. Open existing project

    cd ~/code
    git clone <repo-url>
    cd <repo>

If project is not agent-ready yet, add:

    AGENTS.md
    README.md
    docs/architecture.md

Then run:

    opencode

------------------------------------------------------------

## 4. Which shell to use

    OpenCode    -> main workflow: analyze, plan, fix, review
    Codex       -> ChatGPT subscription agent
    Claude      -> Claude subscription agent
    Gemini      -> Google/Gemini subscription agent

------------------------------------------------------------

## 5. Safe first prompt

For any shell:

    Analyze this project. Do not edit files. Read AGENTS.md, README.md, and docs/architecture.md. Summarize the structure, risks, and next steps.

------------------------------------------------------------

## 6. OpenCode workflow

Inside project:

    opencode

Use:

    /analyze
    /plan <task>
    /review

Rule:

    /analyze before big work
    /plan before edits
    implement manually from the plan in docs/plans/
    /review before commit

------------------------------------------------------------

## 7. Codex workflow

Inside project:

    codex

Safe first prompt:

    Analyze this project. Do not edit files. Read AGENTS.md, README.md, and docs/architecture.md.

Use Codex for:

    OpenAI / ChatGPT subscription model
    second opinion
    implementation planning
    small coding tasks

------------------------------------------------------------

## 8. Claude workflow

Inside project:

    claude

Safe first prompt:

    Analyze this project. Do not edit files. Read AGENTS.md, README.md, docs/architecture.md, and CLAUDE.md.

Use Claude for:

    deep codebase analysis
    architecture review
    documentation
    complex refactor planning

------------------------------------------------------------

## 9. Gemini workflow

Inside project:

    gemini

Safe first prompt:

    Analyze this project. Do not edit files. Read AGENTS.md, README.md, docs/architecture.md, and GEMINI.md.

Use Gemini for:

    alternative opinion
    large-context review
    documentation review
    risk analysis

------------------------------------------------------------

## 10. Before edits

Always check:

    git status

Ask the agent for a plan first.

Do not allow:

    force push
    deleting files
    rm -rf
    editing secrets
    broad unrelated formatting

------------------------------------------------------------

## 11. After edits

Check:

    git status
    git diff

Run relevant verification.

Then commit manually:

    git add .
    git commit -m "message"

Push manually:

    git push

------------------------------------------------------------

## 12. Never commit

    .env
    .env.*
    auth.json
    tokens
    credentials
    API keys
    private keys
    ~/.codex/auth.json
    ~/.claude.json
    ~/.claude/
    ~/.gemini/oauth_creds.json
    ~/.gemini/google_accounts.json
    node_modules/
    *.tar
    *.tar.gz

------------------------------------------------------------

## 13. Backup reminder

Important things not stored in Git:

    WSL export
    Docker volumes
    n8n_data
    Conda full env exports
    local databases
    auth/session files

These belong in encrypted backup / OneDrive / external disk, not project repos.

------------------------------------------------------------
