# CONSTRAINTS.md

## Language & Framework
- Python 3.13+ only. Do not introduce syntax or APIs unavailable in 3.13.
- Django 5.0+ and Django REST Framework. Do not downgrade or pin below these.
- PostgreSQL 16.4+. Do not use SQLite or other databases in any config.

## Forbidden Patterns
- Never hardcode secrets, credentials, or environment-specific values in settings files; use environment variables.
- Never modify `common.py` settings with environment-specific overrides — use `local.py` or `production.py`.
- Do not use `django.contrib.auth.models.User` directly; extend the custom user model already in `users/models.py`.
- Do not add synchronous blocking calls inside async contexts.
- Never commit `.env` files or secrets to the repository.

## Testing Requirements
- Every new view, serializer, and model change must include a corresponding test in the app's `test/` directory.
- Use `factories.py` (factory_boy pattern) for test data — do not use raw `Model.objects.create()` in tests.
- Run tests with: `docker-compose run --rm web pytest`
- PRs with no test changes touching new logic will be rejected.

## Dependency Policy
- Do not add new dependencies without explicit justification in the PR description.
- All dependencies must be added to `pyproject.toml`; do not use a bare `requirements.txt`.
- Prefer stdlib or already-present packages over introducing new ones.

## Off-Limits / Special Care
- `cookiecutter.json` — changes here affect every generated project; treat as a breaking-change surface.
- `{{cookiecutter.app_name}}/users/migrations/` — never hand-edit migration files; generate with `makemigrations`.
- `.github/workflows/push.yaml` — changes must keep CI green; test locally before modifying.
- `wait_for_postgres.py` — do not remove; it is required for Docker startup ordering.

## Structure & Naming
- New Django apps must mirror the `users/` structure: `model.py`, `serializers.py`, `views.py`, `permissions.py`, `admin.py`, `test/__init__.py`, `test/factories.py`, `test/test_views.py`.
- New UI components MUST be imported and rendered in a parent page or component — do not create orphaned components.
- Before creating a new file, search the codebase for existing files with similar purpose — extend existing files instead of duplicating.
- API docs for every new resource must be added to `docs/api/`.
