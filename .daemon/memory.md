# Project Memory

## Stack
- Python 3.13+ / Django 5.0+ / Django REST Framework / PostgreSQL 16.4+ / Docker + docker-compose / pytest / MkDocs / GitHub Actions CI
- Cookiecutter template repo — source files live inside `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/`; path literals with double-braces are Jinja2 template variables, not actual directories

## Gotchas
- The `{{cookiecutter.github_repository_name}}` and `{{cookiecutter.app_name}}` directory names are Cookiecutter placeholders — tools like grep and glob may need escaping or quoting to traverse them
- Multiple overlapping modernization specs exist under `.daemon/specs/` — check all of them before starting a task to avoid duplicating work across `cookiecutter-django-rest-modernization`, `maintenance-dependency-updates`, `maintenance-modernization`, and `modernize-cookiecutter-django-rest`
- `pyproject.toml` is the authoritative config for deps and tooling; no `requirements.txt` should be treated as canonical
- Migrations are committed to the repo and must never be deleted or regenerated from scratch

## First cycle: bootstrap complete.
