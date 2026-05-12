# CONSTRAINTS.md

## Language & Framework Versions
- Python **3.13+** only. Do not introduce syntax or libraries incompatible with 3.13.
- Django **5.0+** and Django REST Framework latest stable.
- PostgreSQL **16.4+** — do not use DB features unavailable in that version.

## Forbidden Patterns
- Never use `requirements.txt` for new dependency declarations — use `pyproject.toml`.
- Never hardcode secrets, credentials, or environment-specific values in any file; use env vars.
- Do not add `print()` debug statements to template source files.
- Never bypass DRF serializer validation by writing directly to the DB in views.
- Do not use deprecated Django 4.x APIs removed in 5.x.

## Testing Requirements
- Every new view **must** have a corresponding test in the `test/` directory of its app.
- Every new serializer **must** have serializer-level tests.
- Use `factory_boy` factories (see `users/test/factories.py`) — never create model instances manually in tests.
- Tests run with: `docker-compose run --rm web pytest`
- PRs with failing or missing tests will be rejected.

## Dependency Policy
- Do not add new Python dependencies without explicit justification in the PR description.
- Prefer extending existing dependencies over introducing new ones.
- All new deps go in `pyproject.toml`; pin to a minimum version, not an exact version.

## Files Requiring Special Care
- `cookiecutter.json` — adding/removing keys is a breaking change; document in PR.
- `{{cookiecutter.app_name}}/config/common.py` — changes affect all generated projects.
- `{{cookiecutter.app_name}}/users/migrations/` — never edit existing migration files.
- `.github/workflows/push.yaml` — CI changes must be tested in a branch first.

## Naming & Style
- Follow PEP 8; use `snake_case` for Python files, variables, and functions.
- New Django apps mirror the `users/` structure exactly: `models.py`, `serializers.py`, `views.py`, `permissions.py`, `admin.py`, `test/`.
- New UI components MUST be imported and rendered in a parent page or component — do not create orphaned components.
- Before creating a new file, search the codebase for existing files with similar purpose — extend existing files instead of duplicating.
