# CONSTRAINTS.md

## Language & Framework
- Python 3.13+ only. No syntax or features below 3.13.
- Django 5.0+ and Django REST Framework — no downgrade.
- PostgreSQL 16.4+ assumed; do not introduce SQLite-specific patterns.

## Forbidden Patterns
- Never use `%`-style string formatting for SQL — use parameterized queries.
- Never hardcode secrets, credentials, or environment-specific values — use env vars via settings.
- Do not use `print()` for logging — use Python `logging` module.
- Never bypass DRF serializer validation by writing directly to the DB in views.
- Do not use `requirements.txt` — dependencies are managed via `pyproject.toml`.

## Testing Requirements
- Every new feature (model, view, serializer) MUST include corresponding tests.
- Tests live in `<app>/test/` following the existing `users/test/` pattern.
- Run tests with: `docker-compose run --rm web pytest`
- Do not merge code that causes existing tests to fail.
- Use `factory_boy` factories (see `users/test/factories.py`) for test data — no raw fixture files.

## Dependency Policy
- Do not add new dependencies without explicit justification in the PR description.
- All new deps go in `pyproject.toml` only.
- Prefer stdlib or already-present packages before introducing new ones.

## Off-Limits / Special Care
- `cookiecutter.json` — changes here affect all generated projects; treat as a public API.
- `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/users/migrations/` — never hand-edit migrations; generate with `makemigrations`.
- `.github/workflows/push.yaml` — CI changes must be tested; don't break the build gate.
- `config/production.py` — production settings are security-sensitive; changes require careful review.

## Structure & Naming
- New Django apps follow the `users/` pattern: model, serializer, view, permissions, urls, test/, migrations/.
- New template features must be reflected in `cookiecutter.json` if they require a new variable.
- Before creating a new file, search the codebase for existing files with similar purpose — extend existing files instead of duplicating.
- New UI components MUST be imported and rendered in a parent page or component — do not create orphaned components.

## Style
- Follow PEP 8. Use consistent 4-space indentation.
- Keep settings DRY — shared config in `common.py`, environment overrides only in `local.py`/`production.py`.
