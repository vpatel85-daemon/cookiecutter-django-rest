# Spec: Maintenance & Dependency Updates

## Goal
Bring cookiecutter-django-rest fully up to date with latest stable versions of all dependencies, modernize tooling, and ensure the test suite passes cleanly after all upgrades.

## Scope
- Upgrade Python to 3.12+
- Upgrade Django to 5.x (latest stable)
- Upgrade Django REST Framework to latest
- Upgrade Celery and all related packages to latest
- Upgrade all other pinned dependencies (dev + prod)
- Update Docker base images to match new Python version
- Adopt ruff for linting/formatting (replaces flake8, isort, black if present)
- Update pre-commit hooks
- Update GitHub Actions to latest action versions
- Fix any tests that fail due to upgraded APIs or removed deprecated features
- Update README if setup steps change

## Done means
All dependencies are on latest stable major versions, CI passes, and the test suite is fully green.
