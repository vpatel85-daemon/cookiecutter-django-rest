# AGENTS.md

## What This Project Does
cookiecutter-django-rest is a Cookiecutter template that scaffolds production-ready Django REST Framework APIs. It generates a fully dockerized project with authentication, user accounts, tests, docs, and CI out of the box. The output is a deployable, scalable REST API with best practices baked in — users clone this repo to bootstrap new services.

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

cookiecutter.json                              # Template variables (inputs)
pyproject.toml                                 # Root tooling config
{{cookiecutter.github_repository_name}}/       # Generated project root
  {{cookiecutter.app_name}}/                   # Django app package
    config/                                    # Settings: common.py, local.py, production.py
    users/                                     # Users app: models, views, serializers, permissions
      migrations/                              # DB migrations
      test/                                    # factories.py, test_views.py, test_serializers.py
    urls.py                                    # Root URL config
    wsgi.py                                    # WSGI entrypoint
  docs/api/                                    # Markdown API docs (authentication, users)
  docker-compose.yml                           # Local dev orchestration
  manage.py                                    # Django management
  conftest.py                                  # pytest root config
.daemon/                                       # Daemon AI agent config
.github/workflows/                             # CI pipeline


## How To Run
bash
# Install template deps
pip install -e .

# Run template tests (validate generated output)
pytest

# Generate a test project
cookiecutter . --no-input

# Inside generated project — start dev server
docker-compose up

# Inside generated project — run tests
docker-compose run --rm web pytest


## Key Patterns
- This is a **Cookiecutter template repo** — source files use `{{cookiecutter.*}}` Jinja2 syntax in paths and file contents. Do not treat template variables as literal strings.
- Settings are split: `common.py` (base), `local.py` (dev), `production.py` (prod). New settings belong in the right layer.
- All new apps inside the generated project follow the `users/` pattern: model → serializer → view → url → test.
- Tests live in `<app>/test/` and use factory_boy factories, not fixtures.
- Config is driven by environment variables; no hardcoded secrets anywhere.

## Where Things Live
- **Template inputs:** `cookiecutter.json`
- **Django settings:** `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/config/`
- **URL routing:** `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/urls.py`
- **DB schema:** migrations in `users/migrations/`
- **CI config:** `.github/workflows/push.yaml`
- **Daemon config:** `.daemon/`
