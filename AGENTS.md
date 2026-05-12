# AGENTS.md

## What This Project Does
cookiecutter-django-rest is a Cookiecutter template that scaffolds production-ready Django REST Framework APIs. It generates a fully dockerized project with authentication, user accounts, tests, API docs, and CI baked in. The output project is immediately deployable and follows Django best practices at scale.

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

cookiecutter.json                            # Template input variables (app_name, github_repository_name, etc.)
{{cookiecutter.github_repository_name}}/     # Generated project root
  {{cookiecutter.app_name}}/
    config/                                  # Django settings: common.py, local.py, production.py
    users/                                   # User model, views, serializers, permissions, migrations, tests
    urls.py                                  # Root URL config
    wsgi.py
  docs/api/                                  # Markdown API docs (authentication.md, users.md)
  conftest.py                                # Pytest fixtures
  docker-compose.yml
  manage.py
  wait_for_postgres.py                       # DB readiness check
.daemon/                                     # Daemon config (constraints, goal, memory, specs)
.github/workflows/push.yaml                  # CI pipeline


## How to Run
- **Build:** `docker-compose build`
- **Dev server:** `docker-compose up`
- **Tests:** `docker-compose run --rm web pytest`
- **Generate a project:** `cookiecutter .` from repo root

## Key Patterns
- All settings are split into `common.py` → `local.py` / `production.py`; never put secrets in `common.py`
- New Django apps go inside `{{cookiecutter.app_name}}/`; mirror the `users/` structure (model, serializer, view, permissions, test/)
- Tests live in `<app>/test/` with `factories.py` for fixtures; use pytest + conftest
- API docs for every new resource go in `docs/api/`
- Template variables are `{{cookiecutter.*}}`; changes to `cookiecutter.json` affect the entire scaffold

## Important File Locations
- **Settings:** `{{cookiecutter.app_name}}/config/`
- **Routes:** `{{cookiecutter.app_name}}/urls.py`
- **DB schema:** migrations in `{{cookiecutter.app_name}}/users/migrations/`
- **CI config:** `.github/workflows/push.yaml`
- **Template inputs:** `cookiecutter.json`
