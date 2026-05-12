# Tasks

## Epic: Dependency Management — uv + pyproject.toml

### Task: Migrate to pyproject.toml with uv
Description: Remove the `requirements/` directory (base.txt, local.txt, production.txt) from the generated project template. Create a `pyproject.toml` with `[project]`, `[project.optional-dependencies]` (dev, prod), and `[tool.uv]` sections. Pin all current deps at their latest stable versions. Add a `uv.lock` to the template.
Acceptance criteria:
- `requirements/` directory is gone from the generated project
- `pyproject.toml` present with all deps correctly categorised
- `uv sync` works inside a freshly generated project
Depends on:

### Task: Update Dockerfile to use uv
Description: Replace `pip install -r requirements/...txt` with `uv sync` in the generated project's `Dockerfile`. Install `uv` via the official method (`pip install uv` or copy from ghcr). Use a `.venv` inside the container or rely on uv's global install behaviour.
Acceptance criteria:
- `docker-compose build` succeeds on a freshly generated project
- Container starts and Django management commands work
Depends on: migrate-to-pyproject-toml-with-uv

---

## Epic: Python & Django Version Bump

### Task: Bump Python to 3.13
Description: Update the generated project's `Dockerfile` base image to `python:3.13-slim`. Add/update `.python-version` to `3.13`. Update `pyproject.toml` `requires-python = ">=3.13"`. Update GitHub Actions matrix to `python-version: ["3.13"]`.
Acceptance criteria:
- Generated project Dockerfile uses python:3.13-slim
- CI passes with Python 3.13
Depends on: update-dockerfile-to-use-uv

### Task: Upgrade Django and DRF to latest stable
Description: In `pyproject.toml`, pin `django` to latest 5.x stable and `djangorestframework` to latest stable. Resolve any compatibility issues in the generated app code (settings, urls, models). Run the generated project's test suite to confirm.
Acceptance criteria:
- `django --version` in the container shows 5.x
- All existing tests pass
Depends on: bump-python-to-3-13

### Task: Upgrade remaining dependencies to latest stable
Description: Audit and upgrade all other pinned packages in `pyproject.toml`: `psycopg2-binary` (or switch to `psycopg[binary]` v3), `gunicorn`, `whitenoise`, `dj-database-url`, `python-decouple`, `pytest-django`, `factory-boy`, `coverage`, `mkdocs`, `mkdocs-material`, and any others present. Resolve conflicts.
Acceptance criteria:
- No packages pinned to outdated versions with known CVEs or major version gaps
- `uv sync` resolves without conflicts
- Test suite passes
Depends on: upgrade-django-and-drf-to-latest-stable

---

## Epic: Linting & Formatting — ruff

### Task: Replace flake8/black/isort with ruff
Description: Remove flake8, black, isort from dev dependencies and delete config files (`.flake8`, any `[tool.black]`/`[tool.isort]` in `setup.cfg` or `pyproject.toml`). Add `ruff` to dev deps. Add `[tool.ruff]` and `[tool.ruff.lint]` config in `pyproject.toml` with rules equivalent to the previous setup (E, F, I). Update pre-commit config if present.
Acceptance criteria:
- `ruff check .` passes on the generated project with no errors
- `ruff format .` produces no diffs
- No references to flake8/black/isort remain
Depends on: upgrade-remaining-dependencies-to-latest-stable

---

## Epic: GitHub Actions CI Modernization

### Task: Modernize GitHub Actions workflows
Description: Update all workflow files in `.github/workflows/` (both the template repo's CI and the generated project's CI). Bump to `actions/checkout@v4`, `actions/setup-python@v5`. Replace pip-tools install steps with `uv sync`. Add `uv` caching. Ensure Python 3.13 matrix. Remove any deprecated `set-output` commands.
Acceptance criteria:
- CI workflow passes end-to-end on a branch
- No deprecated action warnings
Depends on: replace-flake8-black-isort-with-ruff

---

## Epic: Docker & docker-compose Cleanup

### Task: Modernize docker-compose configuration
Description: Update the generated project's `docker-compose.yml`. Drop the top-level `version:` key (deprecated in Compose v2+). Use `postgresql:16` image. Ensure healthchecks are defined for the db service. Confirm `wait_for_postgres.py` still works or replace with a compose `depends_on: condition: service_healthy`.
Acceptance criteria:
- `docker compose up` starts cleanly with no deprecation warnings
- Django app connects to Postgres on startup
Depends on: modernize-github-actions-workflows

---

## Epic: MkDocs & Documentation

### Task: Update MkDocs configuration and dependencies
Description: Bump `mkdocs` and `mkdocs-material` to latest stable in `pyproject.toml`. Update `mkdocs.yml` to use any renamed config keys (e.g. `theme.features`). Fix any broken internal doc links. Ensure `mkdocs build` runs clean.
Acceptance criteria:
- `mkdocs build --strict` exits 0
- No deprecation warnings from mkdocs
Depends on: modernize-docker-compose-configuration

---

## Epic: Bug Fixes & Cleanup

### Task: Audit and fix broken template references
Description: Do a full pass over the cookiecutter template for broken references: incorrect `cookiecutter.*` variable names, missing files referenced in settings or urls, leftover TODO comments, and any Python syntax that's invalid under 3.13. Fix all issues found.
Acceptance criteria:
- `cookiecutter` renders the template without errors
- Generated project passes `python manage.py check --deploy` (with dummy env vars)
Depends on: update-mkdocs-configuration-and-dependencies

### Task: Clean up legacy files and dead code
Description: Remove files that no longer apply: `setup.cfg` (if fully replaced by pyproject.toml), `Makefile` targets that reference removed tools, any `*.pyc` or `__pycache__` entries not in `.gitignore`, and any other dead weight identified during the audit.
Acceptance criteria:
- No references to removed tools anywhere in the repo
- `git status` on a fresh clone shows no untracked junk
Depends on: audit-and-fix-broken-template-references
