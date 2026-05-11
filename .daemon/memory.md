# Project Memory

## Stack
- **Backend template**: Cookiecutter → Django 5.0+ / DRF / PostgreSQL 16.4+ / Docker / pytest
- **Template engine**: Cookiecutter with variables defined in `cookiecutter.json`; folder and file names contain `{{cookiecutter.*}}` placeholders that must be preserved exactly.

## Gotchas
- This is a **Cookiecutter template repo**, not a runnable Django project itself. The actual Django project lives inside `{{cookiecutter.github_repository_name}}/`. Any change to files inside that folder affects *generated* projects, not this repo directly.
- Two levels of context: the template repo root (CI, cookiecutter.json) and the generated project inside the Jinja2-named directories.
- `wait_for_postgres.py` is a startup script for docker-compose health-checking — it is not part of the Django app.
- Settings are split across `common.py` / `local.py` / `production.py` — always check all three before modifying settings-related code.

## History
- First cycle: bootstrap complete.
