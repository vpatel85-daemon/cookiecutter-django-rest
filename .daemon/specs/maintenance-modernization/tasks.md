# Tasks

## Epic: Runtime & Dependencies

### Task: Migrate to pyproject.toml and bump Python to 3.12
Description: Replace setup.cfg/setup.py with a single pyproject.toml. Set requires-python = ">=3.12". Update .python-version file to 3.12.
Acceptance criteria: No setup.cfg or setup.py in repo root. pyproject.toml valid and parseable. .python-version reads 3.12.
Depends on:

### Task: Bump Django to 5.1 and DRF to 3.15
Description: Update requirements files (base.txt, local.txt, production.txt) to pin Django==5.1.x and djangorestframework==3.15.x. Update all directly related packages (django-cors-headers, dj-database-url, django-environ, etc.) to their latest compatible versions.
Acceptance criteria: pip install -r requirements/local.txt succeeds with no conflicts. No Django 4.x or 3.x pins remain.
Depends on: Migrate to pyproject.toml and bump Python to 3.12

### Task: Bump remaining dependencies to latest stable
Description: Update Celery to 5.4.x, kombu, redis client, Pillow, gunicorn, psycopg2, and all other pinned deps to latest stable versions compatible with Django 5.1 and Python 3.12.
Acceptance criteria: All packages at latest stable. pip-audit or safety shows no known CVEs in updated deps.
Depends on: Bump Django to 5.1 and DRF to 3.15

## Epic: Linting & Formatting

### Task: Replace flake8, isort, and black with Ruff
Description: Remove flake8, isort, and black from requirements and config. Add ruff to dev dependencies. Create ruff config section in pyproject.toml covering line length, select rules (E, F, I, UP), and format settings. Remove .flake8, .isort.cfg, and any black config sections.
Acceptance criteria: ruff check . and ruff format . run cleanly on the template. No flake8/isort/black references remain in requirements or config files.
Depends on: Migrate to pyproject.toml and bump Python to 3.12

### Task: Update pre-commit hooks to latest versions
Description: Update .pre-commit-config.yaml to use latest hook versions for all hooks. Replace flake8/isort/black hooks with ruff-pre-commit. Ensure pre-commit run --all-files passes.
Acceptance criteria: .pre-commit-config.yaml uses ruff and ruff-format hooks. All hooks pass on the template codebase.
Depends on: Replace flake8, isort, and black with Ruff

## Epic: Docker & Infrastructure

### Task: Bump Docker base images and Compose config
Description: Update Dockerfile to use python:3.12-slim as base image. Update docker-compose.yml to use postgres:16 and redis:7. Update any docker-compose.override.yml or production compose files. Remove deprecated Compose v2 syntax if present.
Acceptance criteria: docker compose up --build runs without errors. postgres:16 and redis:7 containers start healthy.
Depends on: Bump remaining dependencies to latest stable

## Epic: CI/CD

### Task: Modernize GitHub Actions workflows
Description: Update all workflow files in .github/workflows/ to use actions/checkout@v4, actions/setup-python@v5. Set Python version matrix to 3.12. Remove any deprecated `::set-output` or `::save-state` patterns. Use `pip install uv` + `uv pip install` if beneficial for speed.
Acceptance criteria: All workflow files use v4/v5 actions. Python matrix targets 3.12. No deprecated GitHub Actions syntax.
Depends on: Bump Docker base images and Compose config

## Epic: Code Cleanup

### Task: Remove deprecated Django patterns from template
Description: Replace any META class `app_label` overrides that trigger warnings. Ensure DEFAULT_AUTO_FIELD = 'django.db.models.BigAutoField' is set in base settings. Remove any django.conf.urls.url() usage in favor of re_path or path(). Update MIDDLEWARE and INSTALLED_APPS for Django 5.1 compatibility.
Acceptance criteria: python manage.py check --deploy produces no warnings about deprecated settings or patterns.
Depends on: Bump Django to 5.1 and DRF to 3.15

## Epic: Documentation

### Task: Update README with current versions and setup instructions
Description: Update README.md to reflect Python 3.12, Django 5.1, DRF 3.15. Update badge URLs (Python version, Django version). Refresh quickstart instructions to use the current toolchain (Ruff instead of black/flake8). Remove any outdated references.
Acceptance criteria: All version numbers in README match actual pinned versions. Badges render correctly. Setup instructions work end-to-end on a fresh clone.
Depends on: Modernize GitHub Actions workflows
