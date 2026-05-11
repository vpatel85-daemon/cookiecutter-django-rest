# CONSTRAINTS.md

## Language & Framework
- Python 3.13+ only. Do not introduce syntax or APIs unavailable in 3.13.
- Django 5.0+ and Django REST Framework. Do not downgrade or pin below these.
- PostgreSQL 16.4+ — do not use SQLite-specific features or assumptions.

## Forbidden Patterns
- Never hardcode secrets, credentials, or environment-specific values in settings files — use environment variables.
- Never modify `config/common.py` with environment-specific logic; use `local.py` or `production.py`.
- Do not use raw SQL unless absolutely necessary and justified in the PR description.
- Do not bypass DRF serializers for data validation — all input must be validated through a serializer.
- Do not write tests that instantiate models directly; always use `factories.py` (factory_boy).

## Testing Requirements
- Every new view, serializer, and permission class MUST have corresponding tests.
- Tests live in `<app>/test/test_views.py` and `<app>/test/test_serializers.py` — match this structure for new apps.
- Run tests with: `pytest`
- PRs that reduce test coverage will be rejected.

## Dependency Policy
- Do not add new third-party packages without explicit justification in the PR description.
- Any new dependency must be pinned to a specific version range.
- Prefer extending existing libraries already in the stack over introducing new ones.

## Off-Limits / Special Care
- `cookiecutter.json` — changes affect all generated projects; modify with extreme care and document the impact.
- `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/users/migrations/` — never hand-edit migration files; generate via `makemigrations`.
- `.github/workflows/push.yaml` — CI changes require explicit justification.
- `wait_for_postgres.py` — infrastructure utility; do not modify without understanding docker-compose startup order.

## Naming & Style
- App structure must mirror the `users/` app: `models.py`, `views.py`, `serializers.py`, `permissions.py`, `admin.py`, `migrations/`, `test/`.
- Use snake_case for files/modules, PascalCase for classes.
- New UI components MUST be imported and rendered in a parent page or component — do not create orphaned components.
- Before creating a new file, search the codebase for existing files with similar purpose — extend existing files instead of duplicating.
