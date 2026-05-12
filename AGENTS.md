# AGENTS.md

## What This Project Does
cookiecutter-django-rest is a Cookiecutter template that scaffolds production-ready Django REST Framework APIs. It generates a fully dockerized project with authentication, user accounts, tests, docs, and CI already wired up. Developers clone this repo, run cookiecutter, and get a deployable REST API in seconds.

## Tech Stack
- **Language:** Python 3.13+
- **Framework:** Django 5.0+ / Django REST Framework
- **Database:** PostgreSQL 16.4+
- **Containerization:** Docker + docker-compose
- **Docs:** MkDocs
- **CI:** GitHub Actions (`.github/workflows/push.yaml`)
- **Dependency automation:** pyup (`.pyup.yml`)
- **Build/packaging:** `pyproject.toml`

## Directory Structure

cookiecutter.json                            # Template variables (app_name, github_repository_name, etc.)
{{cookiecutter.github_repository_name}}/     # Generated project root (Jinja2-templated)
  {{cookiecutter.app_name}}/                 # Django application package
    config/                                  # Django settings: common.py, local.py, production.py
    users/                                   # Built-in users app: models, views, serializers, permissions
      migrations/                            # Django migrations
      test/                                  # factories.py, test_views.py, test_serializers.py
    urls.py                                  # Root URL conf
    wsgi.py                                  # WSGI entry point
  docs/api/                                  # Markdown API docs (authentication.md, users.md)
  docker-compose.yml                         # Local dev stack
  conftest.py                                # Pytest fixtures
  manage.py                                  # Django management
  wait_for_postgres.py                       # DB readiness script
.daemon/                                     # Daemon AI agent config
.github/workflows/push.yaml                  # CI pipeline


## How to Run
bash
# Install cookiecutter and scaffold a project
pip install cookiecutter
cookiecutter https://github.com/agconti/cookiecutter-django-rest

# Inside generated project — build and start
docker-compose build
docker-compose up

# Run tests (inside generated project)
docker-compose run --rm web pytest

# Lint/format (template level)
pip install -e .
pytest  # runs template-level tests if present


## Key Patterns
- All changes to the **template** live inside `{{cookiecutter.github_repository_name}}/` — edits here affect every generated project.
- Settings are split: `common.py` (shared) → `local.py` / `production.py` override via inheritance.
- New apps follow the `users/` pattern: model → serializer → view → url → test → factory.
- Tests use `pytest` + `factory_boy` factories; every view and serializer must have coverage.
- Docs for every new endpoint go in `docs/api/`.

## Where Important Things Live
- **Config/settings:** `{{cookiecutter.app_name}}/config/`
- **URL routing:** `{{cookiecutter.app_name}}/urls.py`
- **DB schema:** `{{cookiecutter.app_name}}/users/migrations/`
- **Template variables:** `cookiecutter.json`
- **CI pipeline:** `.github/workflows/push.yaml`
- **Dependency pins:** `pyproject.toml`, `.pyup.yml`
