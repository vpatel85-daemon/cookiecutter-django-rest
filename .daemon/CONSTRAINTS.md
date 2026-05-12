# CONSTRAINTS.md

## Language & Framework Versions
- Python **3.13+** only. Do not introduce syntax or libraries incompatible with 3.13.
- Django **5.0+**. Do not use deprecated Django APIs (e.g., `ugettext`, `url()` patterns).
- PostgreSQL **16.4+**. Do not use DB features unavailable in Postgres 16.

## Cookiecutter Template Rules
- All generated file paths and content referencing project/app names **must** use `{{cookiecutter.variable_name}}` syntax.
- Never hardcode a concrete app name or project name inside template files.
- `cookiecutter.json` is the source of truth for all template variables — do not introduce a new variable without adding it there first.

## Forbidden Patterns
- No `print()` statements in application code — use Python `logging`.
- No hardcoded secrets, credentials, or environment-specific URLs anywhere in the template.
- Never use `AUTH_PASSWORD_VALIDATORS = []` or disable security middleware.
- Do not put environment-specific settings in `config/common.py`.
- Never commit `.env` files.

## Testing Requirements
- Every new feature or bug fix **must** include tests.
- Tests live in `<app>/test/` with `factories.py` for fixtures and `test_<module>.py` files for assertions.
- Run tests with: `docker-compose run --rm web pytest`
- Do not merge code that causes existing tests to fail.

## Dependency Policy
- Do not add new Python dependencies without explicit justification in the PR description.
- Dependencies belong in `pyproject.toml`. Do not use bare `requirements.txt` files unless already present.
- Prefer stdlib or already-present packages over introducing new ones.

## File & Module Discipline
- **Before creating a new file, search the codebase for existing files with similar purpose — extend existing files instead of duplicating.**
- **New Django apps MUST be registered in `INSTALLED_APPS` in `config/common.py` and wired into `urls.py` — do not create orphaned apps or views.**
- Migrations must be generated and committed alongside model changes.
- Do not modify `wait_for_postgres.py` without understanding its role in Docker startup sequencing.

## Style & Naming
- Follow PEP 8. Use snake_case for variables/functions, PascalCase for classes.
- Serializers named `<Model>Serializer`, views named `<Model>ViewSet` or `<Model>View`.
- Test files named `test_<module>.py`. Factory classes named `<Model>Factory`.
- Keep `.daemon/specs/` organized — each spec gets its own subdirectory with `spec.md`, `plan.md`, `tasks.md`, `principles.md`.
