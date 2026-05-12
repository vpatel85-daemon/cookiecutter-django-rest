# Project Memory

## Stack
- Python 3.13+ / Django 5.0+ / Django REST Framework / PostgreSQL 16.4+ / Docker + docker-compose / pytest / MkDocs
- Packaged via `pyproject.toml`; dependency automation via pyup (`.pyup.yml`) and GitHub Actions CI

## Gotchas
- This is a **Cookiecutter template repo** — most source files live inside `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/`. Changes to those files affect every project generated from the template, so treat them as a high-impact surface.
- `cookiecutter.json` defines all template variables; adding or renaming variables is a breaking change for existing users.
- Docker is the expected dev environment; do not assume a local Python environment is set up — always use `docker-compose run --rm web <command>` for one-off commands.
- `wait_for_postgres.py` is a required startup script wired into docker-compose; do not remove it.
- No `package.json` — this is a pure Python project with no Node/JS build tooling.

## First cycle: bootstrap complete.
