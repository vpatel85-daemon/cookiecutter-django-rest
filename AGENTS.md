# AGENTS.md

## What This Project Does
cookiecutter-django-rest is a Cookiecutter template that scaffolds production-ready Django REST Framework APIs in seconds. It generates a fully dockerized project with authentication, user accounts, tests, API docs, and CI pre-wired. The output is a deployable, scalable REST API with best practices baked in.

## Tech Stack
- **Language:** Python 3.13+
- **Framework:** Django 5.0+ with Django REST Framework
- **Database:** PostgreSQL 16.4+
- **Containerization:** Docker + docker-compose
- **Docs:** MkDocs
- **CI:** GitHub Actions (`.github/workflows/push.yaml`)
- **Dependency automation:** pyup (`.pyup.yml`)
- **Testing:** pytest + pytest-django, factory_boy

## Directory Structure

cookiecutter.json                            # Template input variables
pyproject.toml                               # Project/tool config for the template itself
{{cookiecutter.github_repository_name}}/     # Generated project root
  {{cookiecutter.app_name}}/                 # Django app package
    config/                                  # Django settings: common.py, local.py, production.py
    users/                                   # Users app: models, views, serializers, permissions
      migrations/                            # DB migrations
      test/                                  # factories.py, test_views.py, test_serializers.py
    urls.py                                  # Root URL config
    wsgi.py                                  # WSGI entry point
  docs/api/                                  # Markdown API docs (authentication, users)
  docker-compose.yml                         # Local dev services
  manage.py                                  # Django management
  conftest.py                                # Pytest fixtures
  wait_for_postgres.py                       # DB readiness helper
.daemon/specs/                               # Daemon planning specs (multiple active specs)


## How to Run
bash
# Install cookiecutter and generate a project
pip install cookiecutter
cookiecutter https://github.com/agconti/cookiecutter-django-rest

# Inside generated project — build and start
docker-compose build
docker-compose up

# Run tests (inside generated project)
docker-compose run --rm web pytest


## Key Patterns
- All settings split across `config/common.py`, `config/local.py`, `config/production.py` — never put env-specific config in common
- New Django apps follow the `users/` structure: model → serializer → view → urls → test/factories + test_views
- Tests use factory_boy factories (not fixtures) defined in `test/factories.py`
- API views use DRF class-based views; permissions live in `permissions.py` per app
- All new features must ship with corresponding API doc updates in `docs/api/`
- Template variables use `{{cookiecutter.*}}` — never hardcode project/app names inside template files

## Where Things Live
- **Settings:** `{{cookiecutter.app_name}}/config/`
- **Routes:** `{{cookiecutter.app_name}}/urls.py`
- **DB schema:** `{{cookiecutter.app_name}}/users/migrations/`
- **Auth docs:** `docs/api/authentication.md`
- **CI config:** `.github/workflows/push.yaml`
- **Daemon specs:** `.daemon/specs/`
