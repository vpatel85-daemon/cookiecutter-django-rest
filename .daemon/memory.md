# Project Memory

## Stack
- Cookiecutter template → generates Django 5.0+ / DRF / PostgreSQL 16.4+ / Docker projects
- Python 3.13+; pytest + factory_boy for testing; MkDocs for docs; GitHub Actions for CI

## Gotchas
- This is a **template repo**, not a runnable app itself. Files under `{{cookiecutter.github_repository_name}}/` use Jinja2 interpolation and only become real code after `cookiecutter` runs. Always reason about both the template source and the rendered output.
- Multiple overlapping specs exist in `.daemon/specs/` (modernization, dependency updates, maintenance). Check for duplication before starting new work — tasks may already be partially completed.
- `cookiecutter.json` is the canonical list of template variables. Any rename there is a breaking change across the entire template.
- Migrations under `users/migrations/` must be generated, never hand-edited.

## First cycle: bootstrap complete.
