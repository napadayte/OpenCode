# Claude Code

> Шелл от Anthropic. Хорош для большого контекста, рефакторингов, ревью документации.

## Что читает первым

Claude Code читает `CLAUDE.md` в корне проекта:

```markdown
@AGENTS.md

## Claude-specific

Канонический контент в `.opencode/`. Читай по явному пути:
- Агенты: `.opencode/agents/<slug>.md`
- Скиллы: `.opencode/skills/<slug>/SKILL.md`
- Команды: `.opencode/commands/<slug>.md`
- Правила: `.opencode/rules/<slug>.md`
```

`@AGENTS.md` — это директива Claude Code: «загрузить файл AGENTS.md как часть инструкций».

## Конфиг

`.claude/settings.json`:

```json
{
  "permissions": {
    "deny": [
      "Read(./.env)",
      "Read(./auth.json)",
      "Read(./*.key)",
      "Bash(git push --force*)",
      "Bash(git reset --hard*)",
      "Bash(rm -rf*)",
      "Bash(sudo*)"
    ]
  }
}
```

## Формат permissions

Claude Code использует expression format:

```
Read(./path/to/file)       запретить чтение
Bash(command*)             запретить bash паттерн
WebFetch(domain:github.com) запретить webfetch на домен
```

## Где Claude ищет агенты

По умолчанию — `.claude/agents/`. Но у нас всё в `.opencode/`. **Два варианта:**

### Вариант 1 — Простой (рекомендуется)

Просто скажи Claude в чате:

```
Read .opencode/agents/planner.md and act as that agent.
```

Работает всегда. Минус — Claude не покажет агентов в своём `/agent` пикере.

### Вариант 2 — Симлинки (Linux / macOS / WSL)

```bash
cd my-workspace
ln -s ../.opencode/agents   .claude/agents
ln -s ../.opencode/skills   .claude/skills
ln -s ../.opencode/commands .claude/commands
ln -s ../.opencode/rules    .claude/rules
```

Теперь Claude видит всё в своих ожидаемых местах. Источник один — правишь `.opencode/`.

> [!warning]
> Frontmatter в `.opencode/agents/*.md` — **OpenCode-формат**. Если Claude увидит, он проигнорирует поля типа `mode`, `permission`. Зато он спокойно прочитает description и тело. Это OK.

## Когда использовать Claude

- большой контекст (вся кодовая база)
- ревью архитектуры и больших документов
- сложные многошаговые рефакторинги
- работа в Claude.ai web / Claude Code on the Web

## Связано

- [[opencode]] — основной шелл
- [[../концепции/агент]]
