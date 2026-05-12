# CONSTRAINTS.md

## Language & Framework Versions
- Python 3.13+ only — no compatibility shims for older versions
- Django 5.0+ only — do not use deprecated Django APIs
- PostgreSQL 16.4+ — do not introduce SQLite or other DB backends

## Forbidden Patterns
- Never use `%`-style or `.format()` string formatting for SQL — use ORM or parameterized queries
- Never hardcode secrets, credentials, or environment-specific values in any settings file — use environment variables
- Never put environment-specific config in `common.py` — use `local.py` or `production.py`
- Never bypass DRF serializers to write directly to models in views
- Never commit `*.pyc`, `__pycache__`, `.env` files

## Testing Requirements
- Every new view, serializer, or model change MUST include tests
- Tests live in `{{cookiecutter.app_name}}/<resource>/test/` following the `users/test/` structure
- Use factory_boy factories for test data — never raw model `.objects.create()` in tests
- Run tests with: `docker-compose run web pytest`
- PRs without tests for new functionality will be rejected

## Dependency Policy
- Do not add new Python dependencies without explicit justification in the PR description
- All dependencies must be compatible with Python 3.13+ and Django 5.0+
- Update `pyproject.toml` if a dependency is added — do not use bare `requirements.txt` unless it already exists

## Files That Require Special Care
- `cookiecutter.json` — changing variable names here breaks all downstream template references
- `{{cookiecutter.app_name}}/config/production.py` — changes affect live deployments of generated projects
- Migrations — never edit existing migrations; always generate new ones
- `.github/workflows/push.yaml` — CI changes must be tested and justified

## Naming & Style Conventions
- Follow the `users/` app as the canonical pattern for all new resource apps
- New resource apps: `model.py`, `serializers.py`, `views.py`, `permissions.py`, `test/factories.py`, `test/test_views.py`
- API docs required for every new resource: add a markdown file under `docs/api/`

## Integration Rules
- New apps or URL routers MUST be registered in `{{cookiecutter.app_name}}/urls.py` — do not create orphaned views
- Before creating a new file, search the codebase for existing files with similar purpose — extend existing files instead of duplicating
