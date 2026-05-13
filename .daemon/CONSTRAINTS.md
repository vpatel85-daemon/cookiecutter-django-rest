# CONSTRAINTS.md

## Language & Framework
- Python 3.13+ only. Do not introduce syntax or APIs unavailable in 3.13.
- Django 5.0+ and Django REST Framework. No Flask, FastAPI, or other frameworks.
- PostgreSQL 16.4+. No SQLite usage in any non-test context.

## Template Layer Rules
- Files inside `{{cookiecutter.github_repository_name}}/` are Jinja2 templates. Always preserve `{{cookiecutter.*}}` variable syntax — never hardcode values that should be templated.
- All new template variables must be declared in `cookiecutter.json` before use anywhere.
- Do not rename or restructure the `{{cookiecutter.github_repository_name}}/` or `{{cookiecutter.app_name}}/` directory names.

## Forbidden Patterns
- Never use `SECRET_KEY` or credentials hardcoded in any file — use environment variables.
- Never bypass Django's ORM with raw SQL unless absolutely necessary and documented.
- Do not use `print()` for logging — use Python's `logging` module.
- Never use synchronous blocking calls inside async contexts.

## Testing Requirements
- Every new view, serializer, or model must have corresponding tests in the appropriate `test/` directory.
- Use `factory_boy` factories (defined in `test/factories.py`) — never instantiate models directly in tests.
- Run tests with: `docker-compose run web pytest`
- Do not merge code that causes test failures.

## Dependency Policy
- Do not add new dependencies without explicit justification in the PR description.
- All dependencies must be compatible with Python 3.13 and Django 5.0+.
- Prefer packages already present in the template over introducing new ones.

## File & Module Hygiene
- Before creating a new file, search the codebase for existing files with similar purpose — extend existing files instead of duplicating.
- New Django apps or serializers MUST be imported and wired into `urls.py` and settings — do not create orphaned modules.
- `config/common.py` is high-impact; changes there affect all generated projects. Edit with care.

## Style & Naming
- Follow PEP 8. Use snake_case for Python, kebab-case for YAML/markdown filenames.
- App-level test files live in `<app>/test/` and are prefixed `test_` (e.g., `test_views.py`).
- Keep settings split across `common.py`, `local.py`, `production.py` — do not consolidate.
