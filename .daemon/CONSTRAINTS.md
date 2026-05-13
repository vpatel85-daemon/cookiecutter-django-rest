# CONSTRAINTS.md

## Language & Framework
- Python 3.13+ only. No syntax or APIs from older versions.
- Django 5.0+ and Django REST Framework — no deprecated patterns (e.g., no `ugettext`, no `url()` in urlconf).
- PostgreSQL 16.4+ as the only supported database — no SQLite shortcuts in any config.

## Forbidden Patterns
- Never hardcode project or app names inside template files — always use `{{cookiecutter.github_repository_name}}` and `{{cookiecutter.app_name}}`.
- Never put secrets or environment-specific values in `config/common.py` — use `local.py` or `production.py` with env vars.
- Never use `manage.py` shell or raw SQL in migrations — use Django ORM migrations only.
- Do not add `print()` statements to production code — use Python `logging`.
- Never bypass DRF serializer validation by writing directly to model instances in views.

## Testing Requirements
- Every new view, serializer, or model change must include corresponding tests.
- Tests live in `{{cookiecutter.app_name}}/<app>/test/` — file names must be `test_views.py`, `test_serializers.py`, etc.
- Use factory_boy factories (defined in `test/factories.py`) — do not use raw `Model.objects.create()` in tests.
- Run tests with: `docker-compose run --rm web pytest`
- CI must pass before merging — see `.github/workflows/push.yaml`.

## Dependency Policy
- Do not add new dependencies without explicit justification in the PR description.
- All dependencies must be compatible with Python 3.13+ and Django 5.0+.
- Dependency updates are managed by pyup (`.pyup.yml`) — do not manually pin versions without a documented reason.

## File & Module Safety
- `cookiecutter.json` — changes affect all generated projects; modify with extreme care and test generation end-to-end.
- `.github/workflows/push.yaml` — CI changes must not break the build pipeline.
- `config/production.py` — production settings are sensitive; no debug flags, no broad `ALLOWED_HOSTS`.
- `.daemon/specs/` — do not delete or overwrite existing spec files; append or create new specs only.

## Integration Rules
- New Django apps MUST be registered in `INSTALLED_APPS` in `config/common.py` and wired into `urls.py` — do not create orphaned apps.
- Before creating a new file, search the codebase for existing files with similar purpose — extend existing files instead of duplicating.

## Style & Naming
- Snake_case for all Python files, variables, and functions.
- App-level test directories must have an `__init__.py`.
- API doc files must be added to `docs/api/` and referenced in `mkdocs.yml`.
