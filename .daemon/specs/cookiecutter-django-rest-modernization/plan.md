# Technical Plan

## Architecture
This is a cookiecutter template repo. All meaningful changes live inside:
- `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/` — the Django app
- `{{cookiecutter.github_repository_name}}/requirements/` — split requirements files
- `{{cookiecutter.github_repository_name}}/.github/workflows/` — CI config
- `{{cookiecutter.github_repository_name}}/docker-compose.yml` — Docker setup
- `cookiecutter.json` — template defaults

## Approach per epic

### Epic 1 — Dependency Modernization
- Read all requirements files, bump to latest stable
- Add `uv` tooling (pyproject.toml or uv.lock)
- Update `cookiecutter.json` to default Python 3.13, Django 5.1

### Epic 2 — Code Quality & Linting
- Remove flake8/isort/black config files
- Add `ruff.toml` (or `[tool.ruff]` in pyproject.toml) with equivalent rules
- Add `mypy.ini` with `django-stubs` config
- Update `.pre-commit-config.yaml` to use ruff + mypy hooks

### Epic 3 — CI/CD Modernization
- Rewrite `.github/workflows/` to use `uv`, matrix over Python 3.12+3.13 and Django 5.0+5.1
- Pin all `uses:` action versions to latest SHA-pinned tags

### Epic 4 — Django/DRF Best Practices
- Audit settings split (common/local/production) — ensure SECRET_KEY, ALLOWED_HOSTS, DB config are correct
- Replace or add `drf-spectacular` for OpenAPI 3.1 schema
- Add `djangorestframework-simplejwt` with sensible defaults (access + refresh token endpoints)

### Epic 5 — Developer Experience
- Update docker-compose to Compose v2 syntax (no `version:` key, use `depends_on` conditions)
- Improve Makefile: `make install`, `make test`, `make lint`, `make run`
- Update README + MkDocs to reflect all changes

## Key files to touch
- `cookiecutter.json`
- `{{cookiecutter.github_repository_name}}/requirements/*.txt`
- `{{cookiecutter.github_repository_name}}/pyproject.toml` (create if missing)
- `{{cookiecutter.github_repository_name}}/.github/workflows/ci.yml`
- `{{cookiecutter.github_repository_name}}/docker-compose.yml`
- `{{cookiecutter.github_repository_name}}/Makefile`
- Settings files under `config/settings/`
