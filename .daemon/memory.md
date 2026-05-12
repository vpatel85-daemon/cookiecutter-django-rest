# Project Memory

## Stack
- Python 3.13+ / Django 5.0+ / Django REST Framework, PostgreSQL 16.4+, Docker + docker-compose, MkDocs, GitHub Actions CI.
- This is a **cookiecutter template repo** — the actual Django app lives inside `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/`. Most file edits happen inside those templated directories.

## Gotchas
- Paths with `{{cookiecutter.*}}` are Jinja2 template variables — they are literal directory/file names on disk, not rendered values. Treat them as such when reading or writing files.
- There is no `package.json`; this is a pure Python project. No Node tooling.
- `wait_for_postgres.py` is a startup health-check script used inside Docker — it is not a test file.
- Dependency automation is handled by pyup (`.pyup.yml`) in addition to Daemon; avoid duplicate or conflicting update PRs.
- Settings are split three ways (`common`, `local`, `production`) — always check which layer a config key belongs to before editing.

## History
- First cycle: bootstrap complete.
