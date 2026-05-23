# Gemini CLI

> Шелл от Google. Подписка Gemini. Хорош как альтернативное мнение и для большого контекста.

## Что читает первым

Gemini читает `GEMINI.md` в корне проекта:

```markdown
# Gemini CLI Instructions

Follow `AGENTS.md` — same rules and structure apply.

Read first:
- `AGENTS.md`
- `README.md`
- `docs/overview.md`
- `docs/runbook.md`
- `.opencode/rules/dispatch-policy.md`
- `.opencode/rules/workflow.md`

Rules:
- Do not push.
- Do not commit unless explicitly requested.
- Ask before destructive commands.
- Protect secrets, data, backups, databases, Docker volumes, and n8n data.
```

## Конфиг

`.gemini/settings.json`:

```json
{
  "context": {
    "fileName": ["AGENTS.md", "GEMINI.md"]
  }
}
```

`context.fileName` — список файлов, которые Gemini автоматически подгружает.

## Полный список настроек

Gemini поддерживает гораздо больше полей. Самое полезное:

```json
{
  "general": { "preferredEditor": "code" },
  "ui": { "theme": "GitHub" },
  "context": {
    "fileName": ["AGENTS.md", "GEMINI.md"],
    "includeDirectories": ["./docs"],
    "fileFiltering": { "respectGitIgnore": true }
  },
  "model": {
    "name": "gemini-1.5-pro-latest",
    "maxSessionTurns": 10
  },
  "tools": {
    "sandbox": "docker",
    "exclude": ["write_file"]
  }
}
```

| Поле | Что значит |
|---|---|
| `context.fileName` | какие файлы подгружать всегда |
| `context.includeDirectories` | папки-контекст |
| `model.name` | какая модель |
| `tools.sandbox` | изоляция выполнения |
| `tools.exclude` | запретить конкретные tools |

## Запуск

```bash
cd ~/code/my-workspace
gemini
```

## Особенности

- **Богатые настройки.** Можно тонко настроить UI, hooks, MCP servers.
- **Подписка Google.** Если есть Gemini Advanced — доступно из CLI.
- **OAuth.** Авторизация через Google account.

## Что НЕ коммитить

```
~/.gemini/oauth_creds.json
~/.gemini/google_accounts.json
~/.gemini/history/
~/.gemini/tmp/
```

## Когда использовать

- альтернативное мнение от Gemini
- ревью большой документации
- задачи где нужно подписочное Gemini

## Связано

- [[opencode]] — основной шелл
- [[claude-code]] — для refactor'ов
