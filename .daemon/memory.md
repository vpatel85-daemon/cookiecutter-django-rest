# Project Memory

## Stack
- Cookiecutter template → generates Django 5.0+ / DRF REST API projects; Python 3.13+, PostgreSQL 16.4+, Docker.
- Build tooling: `pyproject.toml`, pytest, factory_boy, docker-compose; CI via GitHub Actions.

## Gotchas
- This is a **template repo**, not a runnable app. All meaningful source lives inside `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/` — Jinja2 braces in directory names are intentional and must be preserved exactly.
- `cookiecutter.json` defines all template variables; changes there are breaking changes for downstream users.
- There is no `package.json` — this is a pure Python project; do not assume Node tooling is available.
- `wait_for_postgres.py` is a custom DB readiness script used in docker-compose startup; do not remove it.
- Daemon specs live in `.daemon/specs/` with separate `maintenance-dependency-updates` and `maintenance-modernization` tracks.

## First cycle: bootstrap complete.
