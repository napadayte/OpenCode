# Codex CLI

> Шелл от OpenAI. Использует подписку ChatGPT. Хорош как второе мнение и быстрые проверки в терминале.

## Что читает первым

Codex автоматически читает `AGENTS.md` в корне проекта. Это часть стандарта Codex CLI — он ищет этот файл.

## Конфиг

`.codex/config.toml`:

```toml
# Codex project config
# Keep this file free of secrets.

# Behavior:
#   - Classify first.
#   - Plan before non-trivial changes.
#   - Do not push.
#   - Do not commit unless explicitly requested.
#   - Ask before destructive commands.
```

В шаблоне это комментарии. Codex берёт правила из `AGENTS.md`.

## Глобальный конфиг

`~/.codex/config.toml` — глобальные настройки Codex:

```toml
approval_policy = "on-request"
sandbox_mode = "workspace-write"

[sandbox_workspace_write]
network_access = true
```

| Поле | Что значит |
|---|---|
| `approval_policy` | когда спрашивать одобрение |
| `sandbox_mode` | `workspace-write` = пишет только в проект |
| `network_access` | разрешить интернет |

## Глобальный AGENTS.md (опционально)

`~/.codex/AGENTS.md` — общие правила для всех проектов. Например:

```
- Prefer reading project AGENTS.md first.
- Read docs/architecture.md before architecture changes.
- Do not push.
- Do not commit unless explicitly requested.
- Make small, reviewable changes.
```

## Запуск

```bash
cd ~/code/my-project
codex
```

## Особенности

- **Своих агентов / команд нет** в формате OpenCode. Codex просто использует один LLM и читает `AGENTS.md` как system prompt.
- **Sandbox по умолчанию.** Не запустит произвольный bash без подтверждения.
- **Локальный.** Не пишет в облако.

## Что НЕ коммитить

```
~/.codex/auth.json
~/.codex/history.jsonl
~/.codex/*.sqlite
```

## Когда использовать

- задачи через ChatGPT подписку
- быстрая проверка кода в терминале
- альтернативное мнение от GPT-5
- работа в одном проекте без сложного workflow

## Связано

- [[opencode]] — основной шелл с workflow
- [[claude-code]] — для большого контекста
