# AGENTS.md

## What This Project Does
cookiecutter-django-rest is a project scaffolding template that generates production-ready Django REST Framework APIs. It bootstraps authentication, user accounts, tests, docs, and full Docker-based local dev in seconds. The output is a deployable, scalable REST API with best practices baked in.

## Tech Stack
- **Language:** Python 3.13+
- **Framework:** Django 5.0+ with Django REST Framework
- **Database:** PostgreSQL 16.4+
- **Containerization:** Docker + docker-compose
- **Docs:** MkDocs
- **CI:** GitHub Actions (`.github/workflows/push.yaml`)
- **Dependency automation:** pyup (`.pyup.yml`)

## Directory Structure

cookiecutter.json                          # Template input variables
{{cookiecutter.github_repository_name}}/   # Generated project root
  {{cookiecutter.app_name}}/               # Django app package
    config/                                # Django settings (common, local, production)
    users/                                 # Built-in users app (models, views, serializers, tests)
    urls.py                                # Root URL config
    wsgi.py                                # WSGI entry point
  docs/                                    # MkDocs API documentation
  conftest.py                              # pytest fixtures
  docker-compose.yml                       # Local dev services
  manage.py                                # Django management CLI
  wait_for_postgres.py                     # DB readiness check script
.daemon/specs/                             # Daemon task specs and plans
.github/                                   # Workflows, templates, contributing guide


## How to Run
bash
# Build
docker-compose build

# Dev server
docker-compose up

# Tests
docker-compose run --rm web pytest


## Key Patterns
- Settings split across `config/common.py`, `config/local.py`, `config/production.py` — never put env-specific config in common
- New apps follow the `users/` pattern: models, serializers, views, permissions, and a `test/` subdirectory with factories
- All views go through DRF; no raw Django views
- Factories (via `factory_boy`) live in `test/factories.py` alongside tests
- Migrations must be generated and committed with model changes

## Important Locations
- **Config/Settings:** `{{cookiecutter.app_name}}/config/`
- **URL routing:** `{{cookiecutter.app_name}}/urls.py`
- **DB schema (migrations):** `{{cookiecutter.app_name}}/users/migrations/`
- **CI pipeline:** `.github/workflows/push.yaml`
- **Template variables:** `cookiecutter.json`
