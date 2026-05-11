# CONSTRAINTS.md

## Language & Framework
- Python 3.13+ only — no syntax or patterns from older versions
- Django 5.0+ and DRF latest — do not downgrade or pin to older majors
- PostgreSQL-specific features are acceptable; do not assume SQLite compatibility

## Forbidden Patterns
- Never use `%`-style or `.format()` string formatting in new code — use f-strings
- Never write raw SQL unless absolutely necessary; use the ORM
- Never commit secrets, `.env` files, or credentials
- Never add `print()` debugging to committed code — use Python `logging`
- Never bypass DRF serializer validation by writing directly to the DB in views
- Never modify generated migration files manually — regenerate them with `makemigrations`

## Testing Requirements
- Every new view, serializer, and model method must have corresponding tests
- Tests live in `<app>/test/test_views.py`, `test_serializers.py`, etc.
- Use `factory_boy` factories (see `users/test/factories.py`) — never use fixtures or hardcoded DB inserts
- Run tests with: `docker-compose run --rm web pytest`
- PRs must not reduce test coverage

## Dependency Policy
- Do not add new dependencies without explicit justification in the PR description
- New deps must be added to the appropriate requirements file and pinned to a compatible version range
- Prefer stdlib or already-present packages over introducing new ones

## Off-Limits / Special Care
- `cookiecutter.json` — changes affect all generated projects; modify with extreme care
- `{{cookiecutter.app_name}}/config/production.py` — no debug flags, no insecure defaults ever
- Migrations — never delete or squash without a documented migration plan
- `.github/workflows/push.yaml` — CI changes must be tested and justified

## Naming & Style
- Follow PEP 8; use `snake_case` for files, variables, functions; `PascalCase` for classes
- App names and module names must match the `cookiecutter.app_name` variable convention
- New apps must mirror the structure of the `users` app (model, serializer, views, permissions, test/)

## Integration Rules
- New UI components MUST be imported and rendered in a parent page or component — do not create orphaned components
- Before creating a new file, search the codebase for existing files with similar purpose — extend existing files instead of duplicating
