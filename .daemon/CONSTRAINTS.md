# CONSTRAINTS.md

## Language & Framework
- Python 3.13+ only. No syntax or features from earlier versions.
- Django 5.0+ and Django REST Framework — do not downgrade or pin below these.
- PostgreSQL 16.4+ assumed; do not use SQLite-only features.

## Forbidden Patterns
- Never use raw SQL unless absolutely unavoidable — use Django ORM.
- Never hardcode secrets, credentials, or environment-specific values in any file; use env vars.
- Never use `User.objects.create()` directly in tests — always use factory_boy factories from `test/factories.py`.
- Do not bypass DRF serializers by writing directly to models in views.
- Never modify or delete existing migrations — only add new ones.

## Testing Requirements
- Every new view, serializer, model, or permission change MUST include corresponding tests under the resource's `test/` directory.
- Tests run with: `docker-compose run web pytest`
- PRs without tests for new or changed logic will be rejected.

## Dependency Policy
- Do not add new dependencies without a clear justification in the PR description.
- All deps are managed via `pyproject.toml` — do not use `requirements.txt` as the source of truth.
- Prefer stdlib or already-present packages before introducing new ones.

## Files Requiring Special Care
- `cookiecutter.json` — template variable definitions; changes ripple through all generated file paths.
- `{{cookiecutter.app_name}}/config/common.py` — base settings; modifications affect all environments.
- `.github/workflows/push.yaml` — CI pipeline; do not break the test or lint steps.
- `pyproject.toml` — tooling config; validate after edits.

## Structure & Naming
- New API resources MUST mirror the `users/` structure: `models.py`, `views.py`, `serializers.py`, `permissions.py`, `migrations/`, `test/`.
- New endpoints MUST have a corresponding doc file under `docs/api/`.
- Before creating a new file, search the codebase for existing files with similar purpose — extend existing files instead of duplicating.
- New Django app components MUST be registered in `urls.py` and `config/common.py` — do not create orphaned apps or views.
