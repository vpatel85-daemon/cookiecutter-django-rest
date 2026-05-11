# CONSTRAINTS.md

## Language & Framework Versions
- Python **3.13+** only. No syntax or APIs from older versions.
- Django **5.0+** and Django REST Framework — use their modern idioms.
- PostgreSQL **16.4+** — do not use DB features unavailable in this version.

## Forbidden Patterns
- Never use `%`-style or `.format()` string formatting for SQL — use ORM queries or parameterized queries only.
- Never hardcode secrets, credentials, or environment-specific values in source files — use environment variables.
- Do not add `print()` debug statements; use Python `logging`.
- Do not bypass DRF serializer validation by writing directly to model instances in views.
- Never flatten the settings into a single file — keep the `common/local/production` split.
- Do not use synchronous blocking calls inside async contexts.

## Testing Requirements
- Every new view, serializer, or model change **must** include corresponding tests.
- Tests live in `<app>/test/test_views.py` or `test_serializers.py` — match existing structure.
- Use `factory_boy` factories in `test/factories.py`; do not inline raw fixture data.
- Run tests with: `pytest`
- PRs with failing tests will be rejected.

## Dependency Policy
- Do not add new third-party packages without explicit justification in the PR description.
- Pin versions when adding dependencies; keep consistent with existing requirements files.
- PyUp manages automated dependency updates — do not manually bump versions without reason.

## Off-Limits / Special Care
- `cookiecutter.json` — changes affect all generated projects; modify only intentionally.
- `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/users/migrations/` — never hand-edit migration files; always use `makemigrations`.
- `.github/workflows/push.yaml` — CI config; changes must be tested and justified.
- `{{cookiecutter.app_name}}/config/production.py` — production settings; treat with extreme caution.

## Naming & Style Conventions
- Follow PEP 8. Use `snake_case` for files, variables, and functions; `PascalCase` for classes.
- New apps follow the existing `users` app structure: `models`, `serializers`, `views`, `permissions`, `urls`, `test/`.
- New UI components MUST be imported and rendered in a parent page or component — do not create orphaned components.
- Before creating a new file, search the codebase for existing files with similar purpose — extend existing files instead of duplicating.
