# Tasks: Maintenance & Dependency Updates

## Epic: Runtime & Core Upgrades

### Task: Upgrade Python and Docker base images
Description: Update Dockerfile and docker-compose.yml to use Python 3.12. Update any `.python-version` or `runtime.txt` files if present.
Acceptance criteria:
- Dockerfile uses `python:3.12-slim` (or equivalent)
- docker-compose builds successfully
Depends on:

### Task: Upgrade Django to 5.x
Description: Bump Django to latest stable 5.x in requirements. Fix any breaking changes — middleware, URL conf, model field changes, removed deprecated APIs.
Acceptance criteria:
- Django 5.x installed with no conflicts
- App starts without errors
Depends on: Upgrade Python and Docker base images

### Task: Upgrade Django REST Framework to latest
Description: Bump djangorestframework to latest stable. Address any removed or changed APIs.
Acceptance criteria:
- DRF latest installed
- No import or API errors on startup
Depends on: Upgrade Django to 5.x

### Task: Upgrade Celery and async dependencies
Description: Bump celery, kombu, redis, and any related packages to latest stable versions.
Acceptance criteria:
- Celery worker starts cleanly
- No deprecation errors in Celery config
Depends on: Upgrade Django to 5.x

### Task: Upgrade all remaining dependencies
Description: Bump all other pinned packages in requirements/ (prod, local, test, base) to latest stable. Resolve any conflicts.
Acceptance criteria:
- `pip install` completes with no conflicts
- All requirements files are updated
Depends on: Upgrade Celery and async dependencies

## Epic: Tooling & CI Modernization

### Task: Replace linting tools with ruff
Description: Remove flake8, isort, and black if present. Add ruff with equivalent rule sets. Update setup.cfg or pyproject.toml config. Update pre-commit hooks.
Acceptance criteria:
- `ruff check .` and `ruff format .` run cleanly
- Old linting tools removed from requirements and pre-commit
Depends on: Upgrade all remaining dependencies

### Task: Update GitHub Actions to latest versions
Description: Audit all `.github/workflows/*.yml` files and pin all actions (checkout, setup-python, etc.) to their latest major versions.
Acceptance criteria:
- All workflow action versions are current
- CI runs without deprecation warnings
Depends on:

## Epic: Test Suite Fixes

### Task: Run test suite and fix all failures
Description: Run the full test suite after all upgrades. Identify and fix any test failures caused by API changes, removed features, or changed behavior in upgraded dependencies.
Acceptance criteria:
- All tests pass
- No skipped tests that were previously passing
Depends on: Upgrade all remaining dependencies

### Task: Fix any deprecation warnings surfaced in tests
Description: Address remaining DeprecationWarnings from Django, DRF, or other packages that appear during test runs.
Acceptance criteria:
- Test output is clean of deprecation warnings
- No use of deprecated APIs
Depends on: Run test suite and fix all failures
