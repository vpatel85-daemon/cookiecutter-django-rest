# CONSTRAINTS.md

## Language & Framework
- Python 3.13+ only. No syntax or APIs from older versions.
- Django 5.0+, Django REST Framework latest stable.
- PostgreSQL 16.4+ — no SQLite in any generated output.

## Forbidden Patterns
- Never hardcode secrets, credentials, or environment-specific values — always use environment variables.
- Never use `%`-style string formatting; use f-strings or `.format()` where f-strings aren't possible.
- Do not use `*` imports (`from module import *`).
- Do not add `print()` statements to application code — use Python `logging`.
- Never bypass DRF permissions — every view must declare `permission_classes` explicitly.
- Do not write raw SQL unless absolutely necessary and documented.

## Cookiecutter Template Rules
- All file paths and content inside `{{cookiecutter.github_repository_name}}/` must use valid Jinja2 template syntax for variable substitution. Never hardcode project or app names.
- `cookiecutter.json` is the source of truth for template variables — do not add new variables there without updating all relevant template files.

## Testing Requirements
- Every new view, serializer, or model change must include a corresponding test.
- Tests live in `<app>/test/` following the existing `test_views.py` / `test_serializers.py` pattern.
- Use factory_boy factories (see `users/test/factories.py`) — do not use raw `Model.objects.create()` in tests.
- Run tests with: `docker-compose run --rm web pytest` inside a generated project.
- PRs must not reduce test coverage.

## Dependency Policy
- No new dependencies without explicit justification in the PR description.
- New deps must be added to `pyproject.toml`; do not use bare `requirements.txt` files unless one already exists in the template.
- Prefer stdlib or already-present packages over introducing new ones.

## File & Module Rules
- Before creating a new file, search the codebase for existing files with similar purpose — extend existing files instead of duplicating.
- New UI components MUST be imported and rendered in a parent page or component — do not create orphaned components.
- Settings changes go in the appropriate config layer (`common`, `local`, or `production`) — never in `manage.py` or `wsgi.py`.
- Do not modify `.github/workflows/push.yaml` without understanding the full CI chain.

## Style & Naming
- Follow PEP 8. Use `snake_case` for variables/functions, `PascalCase` for classes.
- App-level modules follow the pattern: `models.py`, `serializers.py`, `views.py`, `permissions.py`, `urls.py`.
- Test files are named `test_<module>.py` and live in `<app>/test/`.
