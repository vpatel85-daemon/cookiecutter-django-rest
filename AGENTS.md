# AGENTS.md

## What This Project Does
cookiecutter-django-rest is a Cookiecutter template that scaffolds production-ready Django REST Framework APIs. It generates authentication, user accounts, tests, docs, and Docker-based local dev in seconds. The output project is deployable, scalable, and follows Django best practices out of the box.

## Tech Stack
- **Language:** Python 3.13+
- **Framework:** Django 5.0+ with Django REST Framework
- **Database:** PostgreSQL 16.4+
- **Containerization:** Docker + docker-compose
- **Docs:** MkDocs
- **CI:** GitHub Actions (`.github/workflows/push.yaml`)
- **Dependency automation:** pyup (`.pyup.yml`)
- **Testing:** pytest + pytest-django, factories via factory_boy

## Directory Structure

cookiecutter.json                            # Template variables (inputs to generation)
pyproject.toml                               # Project-level tooling config
{{cookiecutter.github_repository_name}}/     # Generated project root
  {{cookiecutter.app_name}}/                 # Main Django app package
    config/                                  # Django settings: common.py, local.py, production.py
    users/                                   # User model, serializers, views, permissions, tests
      migrations/                            # DB migrations
      test/                                  # factories.py, test_views.py, test_serializers.py
    urls.py                                  # Root URL config
    wsgi.py                                  # WSGI entry point
  docs/api/                                  # API markdown docs (authentication.md, users.md)
  docker-compose.yml                         # Local dev services (web + postgres)
  manage.py                                  # Django management entry point
  conftest.py                                # Pytest fixtures
.daemon/                                     # Daemon AI agent config and specs
.github/workflows/push.yaml                  # CI pipeline


## How to Run
bash
# Install cookiecutter and generate a project
pip install cookiecutter
cookiecutter https://github.com/agconti/cookiecutter-django-rest

# Inside generated project — build and start dev server
docker-compose up --build

# Run tests (inside generated project)
docker-compose run web pytest


## Key Patterns
- All Django settings split into `common.py`, `local.py`, `production.py` — never put env-specific config in common
- Users app is the canonical reference implementation — follow its structure for new resources (model → migration → serializer → view → urls → test)
- Tests use factories (factory_boy), not fixtures — see `users/test/factories.py`
- Every new resource must have corresponding API docs in `docs/api/`
- Template variables use `{{cookiecutter.*}}` syntax — all generated files live under `{{cookiecutter.github_repository_name}}/`

## Where Important Things Live
- **Settings:** `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/config/`
- **Routes:** `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/urls.py`
- **User model/views:** `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/users/`
- **DB schema:** migrations in `users/migrations/`
- **CI config:** `.github/workflows/push.yaml`
- **Template inputs:** `cookiecutter.json`
