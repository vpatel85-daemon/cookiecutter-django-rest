# Project Memory

## Stack
- Cookiecutter template → generates Python 3.13+ / Django 5.0+ / DRF / PostgreSQL 16.4+ projects.
- Fully dockerized local dev; CI via GitHub Actions; docs via MkDocs; deps in `pyproject.toml`.

## Gotchas
- This repo IS the template — most source files are inside `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/`. Changes to those files affect every project generated from the template, not just this repo.
- Cookiecutter variable syntax (`{{cookiecutter.*}}`) appears in file paths and file contents — do not accidentally strip or escape these when editing.
- Three active spec tracks exist under `.daemon/specs/`: `cookiecutter-django-rest-modernization`, `maintenance-dependency-updates`, and `maintenance-modernization`. Check tasks.md in each before starting new work to avoid duplication.
- `wait_for_postgres.py` is a custom DB readiness probe used in docker-compose startup — it is not a test file.
- Migrations inside the template (`users/migrations/`) are pre-generated stubs; they must remain valid Django migration files.

## First cycle: bootstrap complete.
