# Project Memory

## Stack
- **Template engine:** Cookiecutter with Jinja2-style `{{cookiecutter.*}}` variables in both filenames and file contents — this is not a standard Python project, it is a *template that generates* Python projects.
- **Generated stack:** Python 3.13+ / Django 5.0+ / DRF / PostgreSQL 16.4+ / Docker / pytest / MkDocs

## Gotchas
- Literal double-brace directory names like `{{cookiecutter.github_repository_name}}/` are valid filesystem paths here — they are Cookiecutter template placeholders, not errors.
- There is no `package.json` — this is a pure Python/Django project with no JavaScript frontend.
- `wait_for_postgres.py` is a custom entrypoint health-check script; it is not a test file.
- Settings are environment-split (`common` → `local` / `production`); never consolidate them.
- `.pyup.yml` means dependency PRs may be opened automatically by PyUp — don't conflict with those updates.

## First cycle: bootstrap complete.
