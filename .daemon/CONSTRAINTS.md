# CONSTRAINTS.md

## Language & Framework
- Python 3.13+ only. No compatibility shims for older versions.
- Django 5.0+ and Django REST Framework — no Flask, FastAPI, or other frameworks.
- PostgreSQL 16.4+ is the only supported database; never use SQLite in config.

## Forbidden Patterns
- Never use function-based views; use DRF class-based views (`APIView`, `ModelViewSet`, etc.).
- Never hardcode secrets, credentials, or environment-specific values in any config file.
- Never modify `config/production.py` to reference local/dev resources.
- Never bypass DRF serializers to write directly to models in views.
- Never use `print()` for logging; use Python's `logging` module.

## Testing Requirements
- Every new view, serializer, and model change MUST have corresponding tests.
- Tests live in `<app>/test/test_views.py` and `<app>/test/test_serializers.py`.
- Factories for new models go in `<app>/test/factories.py`.
- Run tests with: `docker-compose run --rm web pytest`
- PRs without tests will be rejected.

## Dependency Policy
- Do not add new Python packages without explicit justification in the PR description.
- Any new dependency must also be reflected in the appropriate requirements file.
- Do not pin to a specific patch version unless there is a known breakage reason.

## Files Requiring Special Care
- `cookiecutter.json` — template variable definitions; changes affect all generated projects.
- `{{cookiecutter.app_name}}/config/common.py` — base settings inherited everywhere; changes have wide impact.
- `{{cookiecutter.app_name}}/users/migrations/` — never hand-edit migrations; always generate via `makemigrations`.
- `.github/workflows/push.yaml` — CI definition; breakage blocks all PRs.

## Naming & Style
- App modules follow the `users/` pattern: `models.py`, `views.py`, `serializers.py`, `permissions.py`, `admin.py`, `__init__.py`, `test/`.
- New Django apps MUST be registered in `config/common.py` `INSTALLED_APPS`.
- New UI components MUST be imported and rendered in a parent page or component — do not create orphaned components.
- Before creating a new file, search the codebase for existing files with similar purpose — extend existing files instead of duplicating.
