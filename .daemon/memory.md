# Project Memory

## Stack
- Cookiecutter template (Python) → generates Django 5.0+ / DRF / PostgreSQL 16.4+ / Docker projects.
- Template-level tooling: pyproject.toml, GitHub Actions CI, pyup for dependency automation.

## Gotchas
- This is a **template repo**, not a runnable app itself. All paths containing `{{cookiecutter.*}}` are Jinja2-style template syntax — they are not Python f-strings and must not be reformatted.
- There are multiple overlapping modernization specs under `.daemon/specs/` (cookiecutter-django-rest-modernization, maintenance-dependency-updates, maintenance-modernization, modernize-cookiecutter-django-rest). Consolidate or defer to the most recent before creating new work.
- `wait_for_postgres.py` is a Docker entrypoint dependency probe — changes here affect container startup ordering.
- Generated project tests live inside the template at `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/users/test/` — these are template files, not directly runnable at the repo root.

## First cycle: bootstrap complete.
