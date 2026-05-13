# CONSTRAINTS.md

## Language & Framework Versions
- Python >= 3.13; do not use syntax or stdlib APIs removed before 3.13.
- Django >= 5.0; Django REST Framework must stay compatible.
- PostgreSQL >= 16.4; do not use DB features unavailable in that version.

## Forbidden Patterns
- Never use `requirements.txt` alone — dependency metadata lives in `pyproject.toml`.
- No function-based Django views; use DRF class-based views or viewsets.
- Never hardcode secrets or credentials anywhere in the template files.
- Do not import with `import *`; always use explicit imports.
- Never bypass migrations — schema changes must have a corresponding migration file.
- Do not modify `cookiecutter.json` variable names without updating every template reference that uses them.

## Testing Requirements
- Every new view, serializer, or model change must include corresponding tests.
- Tests live in `<app>/test/` using pytest + factory_boy; never use Django's `TestCase` fixtures (JSON) for data setup.
- Run tests with: `docker-compose run --rm web pytest`
- PRs with failing tests will be rejected.

## Dependency Policy
- Do not add new dependencies without explicit justification in the PR description.
- All dependencies must be added to `pyproject.toml`; keep them pinned or range-constrained.
- pyup manages automated updates — do not manually update deps en masse.

## Files That Require Special Care
- `cookiecutter.json` — changing variable names breaks all downstream template references.
- `{{cookiecutter.app_name}}/config/common.py` — base settings inherited everywhere; changes affect all environments.
- `.github/workflows/push.yaml` — CI definition; test locally before modifying.
- `wait_for_postgres.py` — startup probe; breakage silently kills Docker startup.

## Naming & Style
- App packages use `snake_case`; follow the `users/` app as the canonical example.
- Every new API resource needs a doc file under `docs/api/<resource>.md`.
- New UI components MUST be imported and rendered in a parent page or component — do not create orphaned components.
- Before creating a new file, search the codebase for existing files with similar purpose — extend existing files instead of duplicating.
