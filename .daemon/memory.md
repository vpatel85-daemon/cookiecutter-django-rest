# Project Memory

## Stack
- Cookiecutter template generating Django 5.0+ / DRF / PostgreSQL 16.4+ / Docker projects; Python 3.13+; pytest + factory_boy for testing; MkDocs for docs.
- CI via GitHub Actions (`push.yaml`); dependency automation via pyup (`.pyup.yml`).

## Gotchas
- This is a **template repo**, not a runnable app itself. All application code lives under `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/` — edits to those files change what gets generated, not a live service.
- `cookiecutter.json` is the source of truth for template variable names — renaming variables there requires updating every `{{cookiecutter.*}}` reference across all template files.
- Multiple overlapping specs exist under `.daemon/specs/` (modernization, dependency-updates, maintenance) — check existing specs before creating new ones to avoid duplication.
- No `package.json` — this is a pure Python/Django project with no JS build step.

## First cycle: bootstrap complete.
