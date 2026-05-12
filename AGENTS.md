# AGENTS.md

## What This Project Does
cookiecutter-django-rest is a Cookiecutter template that scaffolds production-ready Django REST Framework APIs. It generates authentication, user accounts, tests, docs, and Docker-based local dev environments in seconds. The output project is deployable, scalable, and follows best practices out of the box.

## Tech Stack
- **Language:** Python 3.13+
- **Framework:** Django 5.0+ with Django REST Framework
- **Database:** PostgreSQL 16.4+
- **Containerization:** Docker + docker-compose
- **Docs:** MkDocs
- **CI:** GitHub Actions (`.github/workflows/push.yaml`)
- **Dependency automation:** pyup (`.pyup.yml`)
- **Testing:** pytest + pytest-django, factory_boy for fixtures

## Directory Structure

cookiecutter.json                          # Template variables (inputs to scaffolding)
{{cookiecutter.github_repository_name}}/   # Root of the generated project
  {{cookiecutter.app_name}}/               # Django application package
    config/                                # Settings: common.py, local.py, production.py
    users/                                 # User model, views, serializers, permissions
      migrations/                          # DB migrations
      test/                                # factories.py, test_views.py, test_serializers.py
    urls.py                                # Root URL config
    wsgi.py                                # WSGI entry point
  docs/                                    # MkDocs API docs (authentication.md, users.md)
  docker-compose.yml                       # Local dev orchestration
  conftest.py                              # pytest configuration
  manage.py                                # Django management CLI
.daemon/                                   # Daemon agent config and specs
.github/workflows/push.yaml                # CI pipeline


## How to Run
bash
# Install cookiecutter and scaffold a new project
pip install cookiecutter
cookiecutter gh:agconti/cookiecutter-django-rest

# Inside a generated project:
docker-compose up --build        # Build and start all services
docker-compose run web pytest    # Run test suite
docker-compose run web python manage.py runserver  # Dev server (inside container)


## Key Patterns
- All new resources follow the `users/` module pattern: model → migration → serializer → view → url → test
- Settings are split by environment: `common.py` (base), `local.py`, `production.py`
- Tests live in `<app>/test/` with factory_boy factories in `factories.py`
- Template files use `{{cookiecutter.*}}` Jinja2 syntax — do not break interpolation
- Any change to the template must be valid for the generated output, not just the template source

## Where Important Things Live
- **Routes:** `{{cookiecutter.app_name}}/urls.py`
- **Settings:** `{{cookiecutter.app_name}}/config/`
- **User model:** `users/models.py`
- **Auth:** `users/views.py` + `docs/api/authentication.md`
- **Template inputs:** `cookiecutter.json`
- **CI config:** `.github/workflows/push.yaml`
