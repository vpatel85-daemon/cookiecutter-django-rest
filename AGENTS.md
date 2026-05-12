# AGENTS.md

## What This Project Does
cookiecutter-django-rest is a Cookiecutter template that scaffolds production-ready Django REST Framework APIs. It generates a fully dockerized project with authentication, user accounts, tests, docs, and CI baked in. The output is a deployable, scalable REST API — developers add their own resources on top.

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

cookiecutter.json                            # Template input variables (app_name, github_repository_name, etc.)
{{cookiecutter.github_repository_name}}/     # Generated project root
  {{cookiecutter.app_name}}/                 # Django application package
    config/                                  # Django settings: common.py, local.py, production.py
    users/                                   # Built-in users app: models, views, serializers, permissions
      migrations/                            # Django DB migrations
      test/                                  # Per-app tests: factories.py, test_views.py, test_serializers.py
    urls.py                                  # Root URL configuration
    wsgi.py                                  # WSGI entrypoint
  docs/api/                                  # Markdown API docs (authentication.md, users.md)
  docker-compose.yml                         # Local dev orchestration
  conftest.py                                # Pytest configuration and shared fixtures
  wait_for_postgres.py                       # DB readiness probe used in Docker startup
.daemon/                                     # Daemon agent config and specs
.github/workflows/                           # CI pipeline definitions


## How to Run
bash
# Install cookiecutter and generate a project
pip install cookiecutter
cookiecutter gh:agconti/cookiecutter-django-rest

# Inside a generated project — build and start
docker-compose up --build

# Run tests (inside generated project)
docker-compose run --rm web pytest

# Lint / format (template level)
pip install -e .[dev]
pytest  # runs template-level tests if present


## Key Patterns
- **Template variables** use `{{cookiecutter.variable_name}}` — all generated paths and file contents must use this syntax.
- **Settings are split** into `common.py`, `local.py`, `production.py` — never put environment-specific config in `common.py`.
- **Tests live beside the code** they test under a `test/` subdirectory with `factories.py` providing fixtures.
- **Every new app** should follow the `users/` structure: model, serializer, view, permissions, test subdir.
- **Migrations** are committed and versioned inside the template.
- **No hardcoded secrets** — all sensitive values come from environment variables.

## Where Things Live
- **Settings/config:** `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/config/`
- **URL routing:** `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/urls.py`
- **DB schema:** migrations in each app's `migrations/` folder
- **CI pipeline:** `.github/workflows/push.yaml`
- **Template inputs:** `cookiecutter.json`
- **Daemon specs:** `.daemon/specs/`
