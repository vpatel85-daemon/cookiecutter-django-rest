# Project Memory

## Stack
- Cookiecutter template generating Django 5.0+ / DRF / PostgreSQL 16.4+ / Docker projects; Python 3.13+ throughout.
- CI via GitHub Actions; dependency updates via pyup; docs via MkDocs.

## Gotchas
- This is a **template repo**, not a runnable app itself. Files inside `{{cookiecutter.github_repository_name}}/` use Jinja2 `{{cookiecutter.*}}` syntax — treat them as source templates, not normal Python files.
- Multiple overlapping spec folders exist under `.daemon/specs/` (modernization, maintenance, dependency updates) — check for task overlap before starting new work to avoid duplicating effort.
- `cookiecutter.json` is the single source of truth for all template input variables; any new variable must be declared there first.
- Settings are intentionally split across three files (`common`, `local`, `production`) — do not consolidate them.

## First cycle: bootstrap complete.
