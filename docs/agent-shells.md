# Agent Shells Architecture

------------------------------------------------------------

## 0. Назначение

Этот файл описывает архитектуру всех AI coding оболочек, которые будут использоваться в системе:

- OpenCode
- Codex CLI
- Claude Code
- Gemini CLI
- Aider
- IDE / Desktop agents: Cursor, Cline, Continue

Цель:

- не смешивать конфиги разных инструментов;
- иметь общий стандарт проекта;
- хранить безопасные настройки в Git;
- не хранить секреты в Git;
- сделать так, чтобы любой проект можно было открыть любой оболочкой.

------------------------------------------------------------

## 1. Главный принцип

Один проект должен быть понятен разным агентам.

Для этого используется общий слой:

    AGENTS.md
    README.md
    docs/architecture.md

А для отдельных оболочек используются адаптеры:

    .opencode/
    .codex/
    .claude/
    .gemini/
    CLAUDE.md
    GEMINI.md

------------------------------------------------------------

## 2. Базовая структура проекта

Минимальная структура любого проекта:

    project/
    ├── AGENTS.md
    ├── README.md
    ├── docs/
    │   ├── architecture.md
    │   ├── runbook.md
    │   └── decisions/
    │       └── 0001-initial.md
    ├── .gitignore
    └── ...

Расширенная структура для всех оболочек:

    project/
    ├── AGENTS.md
    ├── CLAUDE.md
    ├── GEMINI.md
    ├── README.md
    ├── docs/
    │   ├── architecture.md
    │   ├── runbook.md
    │   └── decisions/
    ├── .opencode/
    │   └── instructions.md
    ├── .codex/
    │   └── config.toml
    ├── .claude/
    │   └── settings.json
    ├── .gemini/
    │   └── settings.json
    └── .gitignore

------------------------------------------------------------

## 3. Общий файл AGENTS.md

`AGENTS.md` — главный общий контракт для всех агентов.

Он должен описывать:

- что это за проект;
- как запускать проект;
- как запускать тесты;
- какие файлы важные;
- какие команды опасные;
- что нельзя менять без разрешения;
- правила архитектуры;
- правила коммитов;
- правила безопасности.

Минимальный смысл:

    AGENTS.md = общий закон проекта

Все остальные файлы должны ссылаться на него.

------------------------------------------------------------

## 4. Общие правила для всех агентов

Любой агент обязан:

1. Сначала изучить проект.
2. Не делать большие переписывания без разрешения.
3. Делать маленькие изменения.
4. Показывать план перед изменениями.
5. Показывать diff после изменений.
6. Не пушить код без прямой команды.
7. Не коммитить без прямой команды.
8. Не удалять файлы без прямого разрешения.
9. Не добавлять зависимости без объяснения.
10. Не трогать secrets, tokens, env-файлы.

------------------------------------------------------------

## 5. OpenCode

------------------------------------------------------------

### 5.1 Назначение

OpenCode — основная терминальная оболочка для работы с проектами в WSL.

Используется для:

- анализа проекта;
- планирования изменений;
- реализации задач;
- ревью diff;
- запуска тестов;
- работы с несколькими агентами;
- project-aware разработки.

------------------------------------------------------------

### 5.2 Где живёт OpenCode

В WSL:

    Binary:
    /home/bohdan/.opencode/bin/opencode

    Global config:
    /home/bohdan/.config/opencode

    Projects:
    /home/bohdan/code

    Config repo:
    git@github.com:napadayte/OpenCode.git

------------------------------------------------------------

### 5.3 Глобальная структура OpenCode

    ~/.config/opencode/
    ├── opencode.json
    ├── AGENTS.md
    ├── .opencode/
    │   └── instructions.md
    ├── docs/
    │   ├── architecture.md
    │   └── agent-shells.md
    ├── agents/
    ├── context/
    ├── projects/
    └── tools/

------------------------------------------------------------

### 5.4 Project-level OpenCode

В проекте можно добавлять:

    project/
    ├── opencode.json
    └── .opencode/
        └── instructions.md

Но по умолчанию лучше начинать только с:

    AGENTS.md
    docs/architecture.md

------------------------------------------------------------

### 5.5 OpenCode workflow

Типовой процесс:

    /analyze
    /plan <task>
    /fix <task>
    /review
    /test

Правило:

    сначала plan
    потом маленькая реализация
    потом review
    потом test

------------------------------------------------------------

## 6. Codex CLI

------------------------------------------------------------

### 6.1 Назначение

Codex CLI — отдельная оболочка для работы с кодом через OpenAI-модели.

Используется как дополнительный агент для:

- анализа;
- генерации кода;
- ревью;
- альтернативного мнения;
- быстрых задач в терминале.

------------------------------------------------------------

### 6.2 Где должен жить Codex

Глобально:

    ~/.codex/

Возможные файлы:

    ~/.codex/config.toml
    ~/.codex/AGENTS.md

В проекте:

    project/
    ├── AGENTS.md
    └── .codex/
        └── config.toml

------------------------------------------------------------

### 6.3 Правило для Codex

Codex должен читать общий проектный контракт:

    AGENTS.md

Если нужен отдельный `.codex/config.toml`, он не должен дублировать всю архитектуру проекта.

Он должен только настраивать поведение Codex.

------------------------------------------------------------

### 6.4 Что можно хранить в Git

Можно:

    .codex/config.toml
    AGENTS.md

Нельзя:

    auth files
    tokens
    API keys
    session files
    local credentials

------------------------------------------------------------

## 7. Claude Code

------------------------------------------------------------

### 7.1 Назначение

Claude Code — отдельная agentic coding оболочка от Anthropic.

Используется для:

- сложного анализа кода;
- больших refactor-планов;
- ревью архитектуры;
- генерации документации;
- реализации задач с длинным контекстом.

------------------------------------------------------------

### 7.2 Где должен жить Claude Code

Глобально:

    ~/.claude/

Возможные файлы:

    ~/.claude/settings.json

В проекте:

    project/
    ├── CLAUDE.md
    ├── AGENTS.md
    └── .claude/
        └── settings.json

------------------------------------------------------------

### 7.3 CLAUDE.md

`CLAUDE.md` — адаптер для Claude Code.

Он не должен дублировать весь `AGENTS.md`.

Он должен говорить:

    Read AGENTS.md.
    Follow docs/architecture.md.
    Do not push.
    Do not commit unless explicitly requested.
    Ask before destructive commands.

------------------------------------------------------------

### 7.4 Минимальный CLAUDE.md

    # Claude Code Instructions

    Follow AGENTS.md.

    Also read:

    - docs/architecture.md
    - docs/runbook.md

    Rules:

    - Do not push.
    - Do not commit unless explicitly requested.
    - Ask before destructive commands.
    - Make small, reviewable changes.
    - Summarize changed files and verification.

------------------------------------------------------------

### 7.5 Что можно хранить в Git

Можно:

    CLAUDE.md
    .claude/settings.json без секретов

Нельзя:

    ~/.claude.json
    auth files
    tokens
    API keys
    credentials

------------------------------------------------------------

## 8. Gemini CLI

------------------------------------------------------------

### 8.1 Назначение

Gemini CLI — дополнительная оболочка для работы с Google Gemini.

Используется для:

- альтернативного анализа;
- генерации идей;
- документации;
- работы с большим контекстом;
- проверки решений другой моделью.

------------------------------------------------------------

### 8.2 Где должен жить Gemini CLI

Глобально:

    ~/.gemini/

Возможные файлы:

    ~/.gemini/settings.json

В проекте:

    project/
    ├── GEMINI.md
    ├── AGENTS.md
    └── .gemini/
        └── settings.json

------------------------------------------------------------

### 8.3 GEMINI.md

`GEMINI.md` — адаптер для Gemini CLI.

Он должен ссылаться на общий контракт:

    AGENTS.md

------------------------------------------------------------

### 8.4 Минимальный GEMINI.md

    # Gemini CLI Instructions

    Follow AGENTS.md.

    Also read:

    - docs/architecture.md
    - docs/runbook.md

    Rules:

    - Do not push.
    - Do not commit unless explicitly requested.
    - Ask before destructive commands.
    - Prefer small changes.
    - Explain risks and verification steps.

------------------------------------------------------------

### 8.5 Что можно хранить в Git

Можно:

    GEMINI.md
    .gemini/settings.json без секретов

Нельзя:

    oauth files
    auth files
    tokens
    API keys
    credentials

------------------------------------------------------------

## 9. Aider

------------------------------------------------------------

### 9.1 Назначение

Aider — терминальный coding assistant, который хорошо подходит для точечных изменений через Git diff.

Используется для:

- маленьких патчей;
- работы с конкретными файлами;
- быстрого исправления багов;
- парного программирования в терминале.

------------------------------------------------------------

### 9.2 Где должен жить Aider

Глобально:

    ~/.aider.conf.yml

В проекте:

    project/
    ├── .aider.conf.yml
    └── AGENTS.md

------------------------------------------------------------

### 9.3 Правило для Aider

Aider должен использоваться для маленьких задач.

Не использовать Aider для:

- массового переписывания проекта;
- удаления больших частей;
- миграций без плана;
- изменений архитектуры без ADR.

------------------------------------------------------------

### 9.4 Что можно хранить в Git

Можно:

    .aider.conf.yml без секретов

Нельзя:

    API keys
    .env
    tokens
    credentials

------------------------------------------------------------

## 10. Cursor

------------------------------------------------------------

### 10.1 Назначение

Cursor — IDE-оболочка для AI-assisted разработки.

Используется для:

- интерактивной работы в редакторе;
- локальных правок;
- объяснения кода;
- работы с UI;
- быстрой навигации по проекту.

------------------------------------------------------------

### 10.2 Project files

В проекте могут быть:

    .cursor/
    AGENTS.md
    docs/architecture.md

Cursor должен следовать тем же правилам:

    Read AGENTS.md.
    Follow docs/architecture.md.
    Do not change secrets.
    Do not rewrite unrelated files.

------------------------------------------------------------

### 10.3 Что можно хранить в Git

Можно:

    .cursor/rules
    .cursor/rules/*.mdc

Нельзя:

    local workspace state
    tokens
    secrets
    credentials

------------------------------------------------------------

## 11. Cline

------------------------------------------------------------

### 11.1 Назначение

Cline — агент внутри VS Code.

Используется для:

- автономных задач;
- браузерных/терминальных действий;
- работы с локальным проектом;
- быстрой реализации фич.

------------------------------------------------------------

### 11.2 Project files

В проекте можно иметь:

    AGENTS.md
    docs/architecture.md

Если появятся отдельные правила Cline, их надо держать отдельно и не смешивать с OpenCode.

------------------------------------------------------------

### 11.3 Правила

Cline не должен:

- пушить без разрешения;
- коммитить без разрешения;
- запускать destructive commands без подтверждения;
- менять `.env`;
- менять production config без задачи.

------------------------------------------------------------

## 12. Continue

------------------------------------------------------------

### 12.1 Назначение

Continue — IDE assistant для VS Code / JetBrains.

Используется для:

- inline completion;
- chat по коду;
- refactor-подсказок;
- локального анализа.

------------------------------------------------------------

### 12.2 Project usage

Continue должен восприниматься как IDE-слой, а не как главный orchestrator.

Главный контракт проекта всё равно:

    AGENTS.md
    docs/architecture.md

------------------------------------------------------------

## 13. Сравнение ролей

------------------------------------------------------------

### 13.1 Основные роли

    OpenCode      -> основной терминальный orchestrator
    Codex CLI     -> OpenAI terminal agent
    Claude Code   -> глубокий анализ и сложные задачи
    Gemini CLI    -> альтернативное мнение и большой контекст
    Aider         -> маленькие Git patches
    Cursor        -> IDE workflow
    Cline         -> VS Code autonomous agent
    Continue      -> IDE assistant / completion

------------------------------------------------------------

### 13.2 Как выбирать инструмент

Для архитектуры:

    OpenCode
    Claude Code

Для реализации маленькой задачи:

    OpenCode
    Aider
    Codex CLI

Для второго мнения:

    Claude Code
    Gemini CLI
    Codex CLI

Для IDE-работы:

    Cursor
    Cline
    Continue

Для документации:

    OpenCode
    Claude Code
    Gemini CLI

------------------------------------------------------------

## 14. Глобальные директории

------------------------------------------------------------

### 14.1 WSL

Основной dev-мир:

    /home/bohdan

Проекты:

    /home/bohdan/code

OpenCode:

    /home/bohdan/.config/opencode
    /home/bohdan/.opencode/bin/opencode

Codex:

    /home/bohdan/.codex

Claude:

    /home/bohdan/.claude

Gemini:

    /home/bohdan/.gemini

Aider:

    /home/bohdan/.aider.conf.yml

------------------------------------------------------------

### 14.2 Windows

Windows home:

    C:\Users\bodec

Windows OpenCode config, если используется:

    C:\Users\bodec\.config\opencode

Но основной вариант:

    запускать coding agents из WSL

------------------------------------------------------------

## 15. Что синхронизируем через Git

------------------------------------------------------------

### 15.1 OpenCode config repo

Repo:

    git@github.com:napadayte/OpenCode.git

Можно хранить:

    opencode.json
    AGENTS.md
    .opencode/instructions.md
    docs/
    agents/
    context/
    tools/
    README.md
    .gitignore

Нельзя хранить:

    auth.json
    tokens
    API keys
    .env
    credentials
    node_modules/
    *.tar
    *.tar.gz
    local session files

------------------------------------------------------------

### 15.2 Project repos

В каждом проекте можно хранить:

    AGENTS.md
    CLAUDE.md
    GEMINI.md
    docs/architecture.md
    docs/runbook.md
    .opencode/instructions.md
    .codex/config.toml
    .claude/settings.json
    .gemini/settings.json
    .aider.conf.yml

Если в файле есть secrets — файл не коммитить.

------------------------------------------------------------

## 16. Что backup-им отдельно

------------------------------------------------------------

Не через Git, а через backup:

    WSL export
    Docker volumes
    n8n_data
    Conda full env exports
    local databases
    binary data
    model caches
    large archives

Пример backup-папки:

    C:\Users\bodec\OneDrive\Backups\dev-system\YYYY-MM-DD_HH-mm

------------------------------------------------------------

## 17. Secrets policy

------------------------------------------------------------

Никогда не коммитить:

    .env
    .env.*
    auth.json
    tokens
    credentials
    API keys
    private keys
    database.sqlite
    n8n_data-backup.tar.gz
    Ubuntu-backup.tar
    ~/.claude.json
    ~/.codex/auth.json
    ~/.gemini/oauth*
    node_modules/

Хранить secrets:

    password manager
    encrypted backup
    local-only env files
    provider dashboards

------------------------------------------------------------

## 18. Универсальный project template

------------------------------------------------------------

Шаблон проекта:

    ~/code/_templates/agent-ready-project

Содержимое:

    agent-ready-project/
    ├── AGENTS.md
    ├── CLAUDE.md
    ├── GEMINI.md
    ├── README.md
    ├── docs/
    │   ├── architecture.md
    │   ├── runbook.md
    │   └── decisions/
    │       └── 0001-initial.md
    ├── .opencode/
    │   └── instructions.md
    ├── .codex/
    │   └── config.toml
    ├── .claude/
    │   └── settings.json
    ├── .gemini/
    │   └── settings.json
    └── .gitignore

------------------------------------------------------------

## 19. Порядок внедрения

------------------------------------------------------------

### Phase 1 — OpenCode

Status:

    In progress

Tasks:

    - [x] Install OpenCode in WSL
    - [x] Create WSL config folder
    - [x] Sync config to GitHub
    - [ ] Validate opencode.json
    - [ ] Test /connect
    - [ ] Test /analyze
    - [ ] Finalize permissions
    - [ ] Finalize commands

------------------------------------------------------------

### Phase 2 — Project template

Status:

    Planned

Tasks:

    - [ ] Create ~/code/_templates/agent-ready-project
    - [ ] Add AGENTS.md
    - [ ] Add docs/architecture.md
    - [ ] Add CLAUDE.md
    - [ ] Add GEMINI.md
    - [ ] Add .gitignore
    - [ ] Add tool-specific folders

------------------------------------------------------------

### Phase 3 — Codex CLI

Status:

    Planned

Tasks:

    - [ ] Install Codex CLI in WSL
    - [ ] Create ~/.codex
    - [ ] Create ~/.codex/config.toml
    - [ ] Add safe project rules
    - [ ] Test on opencode-test project

------------------------------------------------------------

### Phase 4 — Claude Code

Status:

    Planned

Tasks:

    - [ ] Install Claude Code in WSL
    - [ ] Create ~/.claude
    - [ ] Create CLAUDE.md template
    - [ ] Test on opencode-test project

------------------------------------------------------------

### Phase 5 — Gemini CLI

Status:

    Planned

Tasks:

    - [ ] Install Gemini CLI in WSL
    - [ ] Create ~/.gemini
    - [ ] Create GEMINI.md template
    - [ ] Test on opencode-test project

------------------------------------------------------------

### Phase 6 — Aider

Status:

    Planned

Tasks:

    - [ ] Install Aider in WSL
    - [ ] Create .aider.conf.yml template
    - [ ] Test small patch workflow

------------------------------------------------------------

### Phase 7 — IDE agents

Status:

    Planned

Tools:

    - Cursor
    - Cline
    - Continue

Tasks:

    - [ ] Define shared rules
    - [ ] Decide which project files to commit
    - [ ] Prevent secrets from being indexed or committed

------------------------------------------------------------

## 20. Daily workflow

------------------------------------------------------------

### 20.1 New project

    cd ~/code
    mkdir my-project
    cd my-project
    git init

    copy template files
    fill AGENTS.md
    fill docs/architecture.md
    run OpenCode

------------------------------------------------------------

### 20.2 Existing project

    cd ~/code
    git clone <repo-url>
    cd <repo>
    add AGENTS.md
    add docs/architecture.md
    run OpenCode /analyze

------------------------------------------------------------

### 20.3 Before agent changes

Checklist:

    git status
    read AGENTS.md
    read docs/architecture.md
    create plan
    approve plan
    make small changes
    run tests
    review diff

------------------------------------------------------------

### 20.4 After agent changes

Checklist:

    git status
    git diff
    run tests
    update docs if needed
    commit manually
    push manually

------------------------------------------------------------

## 21. Recovery logic

------------------------------------------------------------

If WSL breaks:

    restore from Ubuntu-backup.tar

If OpenCode config breaks:

    git clone git@github.com:napadayte/OpenCode.git ~/.config/opencode

If project breaks:

    git reset / git restore from project repo

If n8n breaks:

    restore n8n_data-backup.tar.gz

If Conda breaks:

    conda env create -f conda-<env>-from-history.yml

------------------------------------------------------------

## 22. Final rule

------------------------------------------------------------

Agents are tools.

Git is memory.

Backup is survival.

AGENTS.md is the project contract.

docs/architecture.md is the map.

No secrets in Git.

No destructive commands without approval.

------------------------------------------------------------
