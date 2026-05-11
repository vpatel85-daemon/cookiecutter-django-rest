# Project Memory

## Stack
- Cookiecutter template → generates Django 5.0+ / DRF / PostgreSQL 16.4+ / Python 3.13+ REST API projects
- Fully dockerized local dev; pytest for testing; MkDocs for docs; GitHub Actions for CI

## Gotchas
- This is a **template repo**, not a runnable app itself — the actual Django project lives inside `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/`. Jinja-style double-brace directory names are literal folder names on disk.
- `cookiecutter.json` is the source of truth for all template variables; any new configurable value must be declared there first.
- Changes to template files affect every project generated from this template — test template rendering when modifying structure.
- `wait_for_postgres.py` is a startup helper script; it is not part of the Django app and should not import Django modules.

## First cycle
Bootstrap complete.
