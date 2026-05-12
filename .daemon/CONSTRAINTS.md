# CONSTRAINTS.md

## Language & Framework Versions
- Python 3.13+ only. No syntax or APIs deprecated before 3.13.
- Django 5.0+. No Django 3.x/4.x-only patterns.
- Django REST Framework must remain the API layer — do not introduce FastAPI, Flask, or alternatives.

## Forbidden Patterns
- Never hardcode secrets, DB URLs, or environment-specific config — use environment variables via Django settings split.
- Never modify `config/production.py` in ways that break twelve-factor app principles.
- Do not add synchronous blocking calls inside async contexts.
- Never use `print()` for logging — use Python's `logging` module.
- Do not break `{{cookiecutter.*}}` template variable syntax in any template file — always validate Jinja2 brackets are intact.

## Testing Requirements
- Every new view, serializer, or model change MUST include a corresponding test in the appropriate `test/` directory.
- Use `factory_boy` for test data — no raw `Model.objects.create()` in tests where a factory can be used.
- Tests run via: `docker-compose run --rm web pytest`
- CI must stay green — do not merge if `.github/workflows/push.yaml` would fail.

## Dependency Policy
- No new dependencies without explicit justification in the PR description.
- All deps must be added to `pyproject.toml` — do not use a bare `requirements.txt` as source of truth.
- pyup (`.pyup.yml`) manages automated version bumps — do not manually pin to outdated versions without a comment explaining why.

## Off-Limits / Special Care
- `cookiecutter.json` — changes here affect all generated projects; treat as a breaking-change surface.
- `users/migrations/` — never hand-edit migration files; always generate via `makemigrations`.
- `wait_for_postgres.py` — do not remove or rename; it is referenced in the Docker entrypoint.
- `.github/workflows/push.yaml` — changes must be tested and must not break CI.

## Naming & Style
- Follow PEP 8. Use `snake_case` for Python identifiers.
- New Django apps inside the template must mirror the `users/` structure exactly.
- New UI components MUST be imported and rendered in a parent page or component — do not create orphaned components.
- Before creating a new file, search the codebase for existing files with similar purpose — extend existing files instead of duplicating.
