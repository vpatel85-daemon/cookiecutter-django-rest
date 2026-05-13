# Project Memory

## Stack
- Cookiecutter template repo (Jinja2 variable paths) → generates Django 5.0+ / DRF / PostgreSQL 16.4+ / Python 3.13+ projects, fully dockerized.
- Root tooling in `pyproject.toml`; generated project tooling lives inside `{{cookiecutter.github_repository_name}}/`.

## Gotchas
- **This is a template, not a runnable app.** Files under `{{cookiecutter.github_repository_name}}/` are Jinja2 templates; `{{cookiecutter.*}}` tokens appear in both file paths and file contents. Never treat them as literal directory names when reasoning about generated output.
- Multiple overlapping spec directories exist under `.daemon/specs/` (modernization, maintenance, dependency-updates) — check tasks.md files before starting new work to avoid duplicating effort.
- The `.pyup.yml` handles automated dependency PRs; do not manually bump deps that pyup already manages unless there's a specific reason.
- No `package.json` — this is a pure Python project with no JS build step.

## First cycle: bootstrap complete.
