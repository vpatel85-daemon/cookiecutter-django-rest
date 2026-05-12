# Specification

## Goal
Modernize cookiecutter-django-rest to be a best-practice Django REST API template in 2024/2025. A developer cloning and running cookiecutter should get Python 3.12, Django 5.1, DRF 3.15, Ruff linting, and a working Docker/CI setup out of the box.

## What "done" looks like
- All deps pinned to latest stable versions
- Ruff replaces flake8/isort/black
- pyproject.toml is the single source of truth for tooling config
- Docker Compose runs cleanly with postgres:16 and redis:7
- GitHub Actions CI passes on Python 3.12
- README reflects actual current versions and setup steps
- No deprecation warnings on `manage.py check`
