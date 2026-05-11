# AGENTS.md

## What This Project Does
cookiecutter-django-rest is a Cookiecutter template that scaffolds production-ready Django REST Framework APIs. It generates a fully dockerized project with authentication, user accounts, tests, and docs out of the box. The goal is to eliminate boilerplate so developers can ship API resources immediately.

## Tech Stack
- **Language:** Python 3.13+
- **Framework:** Django 5.0+ with Django REST Framework
- **Database:** PostgreSQL 16.4+
- **Auth:** Token-based (DRF auth)
- **Testing:** pytest + pytest-django
- **Containerization:** Docker + docker-compose
- **Docs:** MkDocs
- **CI:** GitHub Actions (`.github/workflows/push.yaml`)

## Directory Structure

cookiecutter.json                          # Template variables (app_name, github_repository_name, etc.)
{{cookiecutter.github_repository_name}}/   # The generated project root
  {{cookiecutter.app_name}}/               # Django project package
    config/                                # Settings: common.py, local.py, production.py
    users/                                 # Built-in users app (model, views, serializers, tests)
    urls.py                                # Root URL conf
    wsgi.py                                # WSGI entry point
  docs/                                    # MkDocs API documentation
  docker-compose.yml                       # Local dev stack
  conftest.py                              # pytest fixtures
  manage.py                                # Django management
  wait_for_postgres.py                     # DB readiness helper


## Commands
bash
# Build
docker-compose build

# Dev server
docker-compose up

# Run tests
docker-compose run --rm web pytest

# Generate a project from this template
cookiecutter https://github.com/agconti/cookiecutter-django-rest


## Key Patterns
- All new apps go inside `{{cookiecutter.app_name}}/` alongside `users/`
- Settings are split: `common.py` (base) → `local.py` / `production.py` (overrides)
- Each app should have a `test/` subdirectory with `factories.py` and `test_views.py`
- Use `factory_boy` factories for test data — see `users/test/factories.py`
- Models, serializers, views, and permissions each get their own file per app
- URL patterns are registered in the root `urls.py`
- Migrations live in `<app>/migrations/` and must be committed

## Important File Locations
- **Config/Settings:** `{{cookiecutter.app_name}}/config/`
- **Routes:** `{{cookiecutter.app_name}}/urls.py`
- **DB Schema:** migrations in each app's `migrations/` folder
- **Template variables:** `cookiecutter.json`
- **CI pipeline:** `.github/workflows/push.yaml`
