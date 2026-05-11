# AGENTS.md

## What This Project Does
cookiecutter-django-rest is a project scaffolding template that generates production-ready Django REST API projects. It provides authentication, user account management, tests, docs, and full Docker-based local dev out of the box. Developers run cookiecutter against this template to produce a fully structured API project in seconds.

## Tech Stack
- **Language:** Python 3.13+
- **Framework:** Django 5.0+ with Django REST Framework
- **Database:** PostgreSQL 16.4+
- **Containerization:** Docker + docker-compose
- **Docs:** MkDocs
- **Testing:** pytest (conftest.py at project root)
- **CI:** GitHub Actions (`.github/workflows/push.yaml`)
- **Deps automation:** PyUp (`.pyup.yml`)

## Directory Structure

cookiecutter.json                          # Template variables (app_name, github_repository_name, etc.)
{{cookiecutter.github_repository_name}}/   # Generated project root
  {{cookiecutter.app_name}}/               # Django app package
    config/                                # Django settings: common.py, local.py, production.py
    users/                                 # Built-in users app: models, views, serializers, permissions, tests
      migrations/                          # DB migrations
      test/                                # factories.py, test_views.py, test_serializers.py
    urls.py                                # Root URL conf
    wsgi.py                                # WSGI entry point
  docs/                                    # MkDocs API documentation
  docker-compose.yml                       # Local dev environment
  conftest.py                              # pytest configuration
  manage.py                                # Django management
  wait_for_postgres.py                     # DB readiness helper


## Commands
bash
# Build / start local environment
docker-compose up --build

# Run tests (inside container or virtualenv)
pytest

# Django dev server (without Docker)
python manage.py runserver

# Apply migrations
python manage.py migrate


## Key Patterns
- **Template variables** appear as `{{cookiecutter.variable_name}}` in filenames and file contents — always preserve this syntax.
- Settings are split by environment: `common.py` → `local.py` / `production.py`.
- Each resource follows the pattern: `models.py → serializers.py → views.py → urls.py` with a matching `test/` directory.
- Test factories live in `test/factories.py` (factory_boy pattern); do not inline fixture data.
- Migrations are committed; always generate them when changing models.

## Important Locations
- **Config/settings:** `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/config/`
- **Routes:** `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/urls.py`
- **DB schema:** migrations in each app's `migrations/` folder
- **Template inputs:** `cookiecutter.json`
- **CI pipeline:** `.github/workflows/push.yaml`
