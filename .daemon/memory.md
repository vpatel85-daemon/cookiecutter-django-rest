# Project Memory

## Stack
- Python 3.13+ / Django 5.0+ / Django REST Framework — Cookiecutter template repo, not a runnable app itself.
- Generated projects use PostgreSQL 16.4+, Docker + docker-compose, pytest, factory_boy, MkDocs, GitHub Actions CI.

## Gotchas
- This is a **template repo**: most source lives inside `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/`. Jinja-style `{{...}}` in filenames and file contents are template variables, not errors.
- `cookiecutter.json` is the single source of truth for variable names — changes there cascade everywhere.
- There are multiple overlapping specs in `.daemon/specs/` (modernization, dependency-updates, maintenance-modernization, modernize-cookiecutter-django-rest). Consolidate and avoid duplicate work across them.
- `wait_for_postgres.py` is a startup dependency — if broken, Docker compose silently hangs.

## First cycle: bootstrap complete.
