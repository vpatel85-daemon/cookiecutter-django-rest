# Project Memory

## Stack
- Cookiecutter template → generates Django 5.0+ / DRF / PostgreSQL 16.4+ / Docker projects; Python 3.13+.
- CI via GitHub Actions; dependency updates via pyup; docs via MkDocs.

## Gotchas
- This is a **template repo**, not a runnable Django project itself. The actual Django code lives inside `{{cookiecutter.github_repository_name}}/` — double-check you're editing template files vs. the template wrapper.
- Multiple overlapping specs exist in `.daemon/specs/` (modernization, dependency-updates, maintenance) — check all before starting work to avoid duplicate effort.
- `wait_for_postgres.py` is a custom DB readiness script used in docker-compose startup; don't remove or replace it with a bare `sleep`.
- Template variable syntax `{{cookiecutter.*}}` must be preserved exactly in file paths and file contents — Jinja2-style; breaking this breaks project generation.

## First cycle
Bootstrap complete.
