# AGENTS.md

## What This Project Does
cookiecutter-django-rest is a Cookiecutter template that scaffolds production-ready Django REST Framework APIs. It generates auth, user accounts, tests, Docker dev environment, and MkDocs documentation in seconds. The output project is deployable, scalable, and follows Django best practices out of the box.

## Tech Stack
- **Language:** Python 3.13+
- **Framework:** Django 5.0+ / Django REST Framework
- **Database:** PostgreSQL 16.4+
- **Containerization:** Docker + docker-compose
- **Docs:** MkDocs
- **CI:** GitHub Actions (`.github/workflows/push.yaml`)
- **Dependency automation:** pyup (`.pyup.yml`)
- **Testing:** pytest + pytest-django (`conftest.py` at project root)

## Directory Structure

cookiecutter.json                            # Template variables (app_name, github_repository_name, etc.)
pyproject.toml                               # Root tooling config (linting, formatting, pytest)
{{cookiecutter.github_repository_name}}/     # Generated project root
  {{cookiecutter.app_name}}/
    config/                                  # Django settings: common.py, local.py, production.py
    users/                                   # User model, serializers, views, permissions, tests
      migrations/                            # DB migrations
      test/                                  # factories.py, test_views.py, test_serializers.py
    urls.py                                  # Root URL conf
    wsgi.py
  docs/api/                                  # Markdown API docs (authentication.md, users.md)
  docker-compose.yml
  manage.py
  wait_for_postgres.py                       # Startup health-check script
.daemon/specs/                               # Daemon task specs and plans


## How To Run
bash
# Install cookiecutter and generate a project
pip install cookiecutter
cookiecutter https://github.com/agconti/cookiecutter-django-rest

# Inside generated project — build and start
docker-compose up --build

# Run tests (inside generated project)
docker-compose run --rm web pytest

# Lint / format (root repo)
pip install -e ".[dev]"
ruff check . && ruff format .


## Key Patterns
- All Django settings split across `config/common.py` → `local.py` / `production.py`; never put secrets in common.
- New resources follow the `users/` pattern: model → serializer → view → URL registration → test factory → test file.
- Tests live in `<app>/test/` with a `factories.py` using `factory_boy`; always write both serializer and view tests.
- Template files use `{{cookiecutter.*}}` Jinja2 variables — keep all generated paths inside `{{cookiecutter.github_repository_name}}/`.
- API docs are Markdown files under `docs/api/`; add a doc file for every new endpoint group.

## Important File Locations
- **Settings:** `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/config/`
- **URL routes:** `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/urls.py`
- **DB schema:** migrations in `users/migrations/`; add new app migrations under `<app>/migrations/`
- **CI config:** `.github/workflows/push.yaml`
- **Template inputs:** `cookiecutter.json`
