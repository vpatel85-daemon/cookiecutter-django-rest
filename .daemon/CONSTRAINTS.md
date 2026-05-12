# CONSTRAINTS.md

## Language & Framework
- Python 3.13+ only. No syntax or features from older versions.
- Django 5.0+ and Django REST Framework — no legacy patterns (e.g., no `url()`, use `path()`)
- PostgreSQL 16.4+ assumed; do not introduce SQLite-specific behavior

## Template Rules
- Never break `{{cookiecutter.*}}` Jinja2 interpolation syntax in template files
- Changes must produce valid, runnable output after scaffolding — test mentally both the template source AND the rendered output
- `cookiecutter.json` is the single source of truth for template variables; do not hardcode values that should be parameterized

## Forbidden Patterns
- Never use `%`-style string formatting for Django queries — use ORM methods
- No raw SQL unless absolutely necessary and reviewed
- Do not add `print()` debug statements to template source files
- Never commit secrets, tokens, or credentials — use environment variables
- Do not use `os.environ[]` (raises on missing); use `os.environ.get()` or `django-environ`

## Testing Requirements
- Every new view, serializer, or model change MUST include corresponding tests in `<app>/test/`
- Use factory_boy factories (see `users/test/factories.py`) for test data — no bare `Model.objects.create()` in tests
- Run tests with: `docker-compose run web pytest`
- All tests must pass before a PR is mergeable

## Dependency Policy
- Do not add new dependencies without explicit justification in the PR description
- New deps must be added to `pyproject.toml` — do not use `requirements.txt` as the source of truth
- Prefer stdlib or already-present libraries before pulling in new packages

## Off-Limits / Special Care
- `users/migrations/` — never hand-edit migrations; generate with `makemigrations`
- `.github/workflows/push.yaml` — CI changes require extra caution; do not break the pipeline
- `cookiecutter.json` — variable renames cascade everywhere; treat as a breaking change

## Code Organization
- New Django apps follow the `users/` module pattern: model, serializer, view, urls, test/
- Before creating a new file, search the codebase for existing files with similar purpose — extend existing files instead of duplicating
- New UI components or template partials MUST be imported and rendered in a parent page or component — do not create orphaned components

## Style
- Follow PEP 8; use existing code style as the reference
- Class-based views preferred (see `users/views.py`) over function-based views
