# Python UV Project Template (Copier)

Шаблон Copier для быстрого старта Python‑проекта с `uv`, Ruff, pre-commit, EditorConfig и готовыми рекомендациями для VS Code.

## Требования
- Python 3.9+
- [copier](https://copier.readthedocs.io/) (`pipx install copier`)
- [proto](https://moonrepo.dev/proto) для установки `uv`

## Как использовать
1. Склонируйте репозиторий или укажите путь к шаблону.
2. Сгенерируйте проект:
   ```bash
   copier copy --trust gh:TiMirLAN/pyup-template ./my-project
   ```
3. Ответьте на вопросы:
   - `project_name` — имя проекта (по умолчанию название папки).
   - `project_description` — описание проекта.
   - `init_git_repo` — инициализировать git?
   - `init_uv_environment` — настроить окружение через `uv`?
   - `uv_type` — тип проекта (`app`, `lib`, `script`, если выбран `uv`).
   - `uv_use_package` — настроить окружение для сборки python-пакета (для `uv`).
   - `install_tool_ruff` — установить Ruff.
   - `install_tool_pre_commit` — установить pre-commit (если есть git).

## Что делает шаблон
- Генерирует базовую структуру через `uv init` с описанием и выбранным типом проекта.
- Создаёт виртуальное окружение `uv venv`.
- Устанавливает Ruff и pre-commit (через `uv tool install` или `pipx`, если `uv` не выбран).
- Инициализирует git (по желанию) и включает pre-commit хуки, запускает проверку `pre-commit run --all-files`.
- Добавляет готовые конфиги: `.pre-commit-config.yaml`, `.ruff.toml`, `.editorconfig`, `.gitignore`, настройки VS Code с рекомендациями расширений.

## Полезные команды после генерации
- Запуск форматирования и lint: `pre-commit run --all-files`
- Обновление окружения: `uv sync`
- Установка доп. инструментов: `uv tool install <pkg>`

## Лицензия
MIT (при необходимости добавьте файл LICENSE в сгенерированный проект).
