# CONSTRAINTS.md

## Language & Framework Versions
- Python **3.13+** only. No syntax or APIs deprecated before 3.13.
- Django **5.0+** only. Do not use patterns removed in Django 4.x or earlier.
- Django REST Framework latest stable. No DRF 2.x patterns.
- PostgreSQL **16.4+** — do not use DB features unavailable in that version.

## Forbidden Patterns
- Never use `%`-style string formatting in SQL or logging — use parameterized queries or f-strings.
- Never commit secrets, `.env` files, or credentials to the template or generated project.
- Do not add synchronous blocking code inside async views (project may adopt async Django views).
- Never hardcode `DEBUG=True` outside of `config/local.py`.
- Do not bypass DRF permissions — every view must declare `permission_classes` explicitly.

## Testing Requirements
- Every new view **must** have a corresponding test in `<app>/test/test_views.py`.
- Every new serializer **must** have a corresponding test in `<app>/test/test_serializers.py`.
- New model fixtures go in `<app>/test/factories.py` using `factory_boy`.
- Run tests with: `docker-compose run --rm web pytest`
- PRs must not reduce test coverage.

## Dependency Policy
- No new `pip` dependencies without explicit justification in the PR description.
- All dependencies must be pinned or range-pinned in `pyproject.toml`.
- Prefer stdlib or already-present packages before adding new ones.
- pyup manages automated updates — do not manually loosen pins without reason.

## Off-Limits / Special Care Files
- `cookiecutter.json` — changes affect all generated projects; treat as a breaking-change surface.
- `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/users/migrations/` — never hand-edit migration files; generate via `manage.py makemigrations`.
- `.github/workflows/push.yaml` — CI changes must be tested; do not disable steps.
- `pyproject.toml` (root) — tooling config shared across the template repo itself.

## Naming & Style
- Follow PEP 8; use `ruff` for linting and formatting (configured in `pyproject.toml`).
- New Django apps use `snake_case`; serializers/views follow DRF naming conventions (`<Resource>Serializer`, `<Resource>ViewSet`).
- New Cookiecutter variables in `cookiecutter.json` must be `snake_case`.

## Integration Rules
- **Before creating a new file, search the codebase for existing files with similar purpose — extend existing files instead of duplicating.**
- **New URL patterns MUST be registered in `urls.py` — do not create orphaned views with no route.**
- New API endpoint groups MUST have a corresponding Markdown doc added under `docs/api/`.
