# AGENTS.md

## What This Project Does
cookiecutter-django-rest is a Cookiecutter template that scaffolds production-ready Django REST Framework APIs. It generates a fully dockerized project with authentication, user accounts, tests, docs, and CI baked in. The output is a deployable, scalable REST API — developers add their own resources on top.

## Tech Stack
- **Language:** Python 3.13+
- **Framework:** Django 5.0+ + Django REST Framework
- **Database:** PostgreSQL 16.4+
- **Containerization:** Docker + docker-compose
- **Docs:** MkDocs
- **CI:** GitHub Actions (`.github/workflows/push.yaml`)
- **Dependency automation:** pyup (`.pyup.yml`)
- **Testing:** pytest + pytest-django + factory_boy

## Directory Structure

cookiecutter.json                            # Template variables (app_name, github_repository_name, etc.)
pyproject.toml                               # Root dev tooling / lint config
{{cookiecutter.github_repository_name}}/     # Generated project root
  {{cookiecutter.app_name}}/                 # Django project package
    config/                                  # Settings: common.py, local.py, production.py
    users/                                   # Built-in users app (model, views, serializers, permissions)
      migrations/                            # DB migrations
      test/                                  # factories.py, test_views.py, test_serializers.py
    urls.py                                  # Root URL conf
    wsgi.py                                  # WSGI entry point
  docs/api/                                  # Markdown API docs (authentication.md, users.md)
  docker-compose.yml                         # Local dev stack
  conftest.py                                # pytest fixtures
  manage.py                                  # Django CLI
  wait_for_postgres.py                       # DB readiness probe
.daemon/                                     # Daemon config and specs
.github/workflows/push.yaml                  # CI pipeline


## How to Run
bash
# Install cookiecutter and generate a project
pip install cookiecutter
cookiecutter gh:agconti/cookiecutter-django-rest

# Inside generated project — build and start
docker-compose build
docker-compose up

# Run tests (inside generated project)
docker-compose run --rm web pytest


## Key Patterns
- All new apps follow the `users/` structure: model, serializer, permissions, views, and a `test/` subpackage with factories and test files.
- Settings are split into `common.py` → `local.py` / `production.py`; never put secrets in `common.py`.
- Use `factory_boy` for test data; never create fixtures manually.
- API views use DRF class-based views or viewsets; no function-based views.
- Every new endpoint needs a corresponding doc file under `docs/api/`.

## Where Important Things Live
- **Settings:** `{{cookiecutter.app_name}}/config/`
- **URL routing:** `{{cookiecutter.app_name}}/urls.py`
- **DB schema:** migrations under each app's `migrations/`
- **Auth logic:** `users/views.py`, `users/permissions.py`
- **Template variables:** `cookiecutter.json`
- **CI config:** `.github/workflows/push.yaml`
