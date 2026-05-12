# Project Memory

## Stack
- Cookiecutter template repo → generates Django 5.0+ / DRF / PostgreSQL 16.4+ / Docker projects in Python 3.13+.
- Root repo tooling (lint, format, pytest) configured via `pyproject.toml`; generated project tooling lives inside `{{cookiecutter.github_repository_name}}/`.

## Gotchas
- **Double-layer structure:** the repo itself is not a Django project. All Django code lives inside the `{{cookiecutter.*}}` template directories — be careful not to confuse root-level files with generated-project files.
- **Jinja2 path names:** file paths containing `{{cookiecutter.github_repository_name}}` and `{{cookiecutter.app_name}}` are literal directory names on disk, not rendered — Cookiecutter processes them at generation time.
- Multiple overlapping specs exist in `.daemon/specs/` (modernization, dependency-updates, maintenance-modernization, modernize-cookiecutter-django-rest) — consolidate and avoid duplicating work across them.
- `wait_for_postgres.py` is a custom health-check script required before Django starts in Docker; do not remove it.

## First Cycle
Bootstrap complete.
