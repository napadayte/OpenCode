# OpenCode

> Основной шелл. Сюда положен главный workflow и все агенты/скиллы.

## Конфиг

`opencode.json` в корне проекта:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "default_agent": "planner",
  "instructions": [
    "AGENTS.md",
    ".opencode/instructions.md",
    ".opencode/rules/dispatch-policy.md",
    ".opencode/rules/workflow.md"
  ],
  "permission": {
    "*": "ask",
    "read": "allow",
    "edit": "ask",
    "bash": {
      "*": "ask",
      "git status*": "allow",
      "git push*": "deny",
      "rm -rf *": "deny"
    }
  }
}
```

## Где живут агенты и команды

```
.opencode/
├── agents/<slug>.md           ← OpenCode сам сканирует
├── skills/<slug>/SKILL.md     ← и тут
├── commands/<slug>.md         ← и тут
└── rules/<slug>.md            ← читаются по AGENTS.md
```

> [!important]
> Никаких `agent:` или `command:` блоков в `opencode.json` не нужно. Файлы автоматически подхватываются через `Glob.scan("{agent,agents}/**/*.md")`.

## Permission система

`permission` — основа безопасности. Три значения:

| Действие | Что делает |
|---|---|
| `allow` | разрешено без вопросов |
| `ask` | спросит подтверждение |
| `deny` | запрещено |

Шаблон workspace ставит `*: ask` глобально и точечно разрешает безопасные команды (`git status*`, `ls *`, ...).

## Запуск

```bash
cd ~/code/my-workspace
opencode
```

Внутри:

```
/analyze         ориентировка
/plan <task>     план задачи
/review          проверка диффа
```

## Built-in агенты

OpenCode идёт с дефолтными: `build`, `plan`, `general`, `explore`. В workspace мы добавляем свои сверху (`planner`, `reviewer`, ...). Через `default_agent: planner` указываем какой запускается по умолчанию.

## Связано

- [[../концепции/агент]]
- [[../концепции/команда]]
- [[../структура-файлов]]
