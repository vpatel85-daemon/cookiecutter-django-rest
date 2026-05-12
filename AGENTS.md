# AGENTS.md

## What This Project Does
cookiecutter-django-rest is a Cookiecutter template that scaffolds production-ready Django REST Framework APIs. It generates authentication, user accounts, tests, docs, and Docker-based local dev from a single `cookiecutter.json` config. The output is a deployable, scalable REST API with best practices baked in.

## Tech Stack
- **Language:** Python 3.13+
- **Framework:** Django 5.0+ with Django REST Framework
- **Database:** PostgreSQL 16.4+
- **Containerization:** Docker + docker-compose
- **Docs:** MkDocs
- **CI:** GitHub Actions (`.github/workflows/push.yaml`)
- **Dependency automation:** pyup (`.pyup.yml`)
- **Packaging:** `pyproject.toml`

## Directory Structure

cookiecutter.json                          # Template variables (app_name, github_repository_name, etc.)
{{cookiecutter.github_repository_name}}/   # Generated project root
  {{cookiecutter.app_name}}/               # Django app package
    config/                                # Django settings: common.py, local.py, production.py
    users/                                 # User model, serializers, views, permissions, migrations
      test/                                # factories.py, test_views.py, test_serializers.py
    urls.py                                # Root URL configuration
    wsgi.py                                # WSGI entrypoint
  docs/api/                                # Markdown API docs (authentication.md, users.md)
  docker-compose.yml                       # Local dev orchestration
  conftest.py                              # Pytest root fixtures
  manage.py                                # Django management entrypoint
.daemon/                                   # Daemon agent config and specs
.github/workflows/push.yaml                # CI pipeline


## How to Run
bash
# Install template deps
pip install -e .

# Scaffold a new project
cookiecutter .

# Inside generated project — start dev environment
docker-compose up --build

# Run tests (inside generated project)
docker-compose run --rm web pytest


## Key Patterns
- All new Django apps follow the `users/` structure: `models.py`, `serializers.py`, `views.py`, `permissions.py`, `admin.py`, `migrations/`, `test/`.
- Settings split across `config/common.py` (base), `config/local.py`, `config/production.py` — never hardcode env-specific values.
- Tests use `pytest` + `factory_boy` factories — all new views and serializers must have corresponding tests.
- Cookiecutter variables live in `cookiecutter.json` — template files use `{{cookiecutter.*}}` syntax.
- `wait_for_postgres.py` is used in Docker entrypoint — do not remove it.
