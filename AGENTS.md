# AGENTS.md

## What This Project Does
cookiecutter-django-rest is a Cookiecutter template that scaffolds production-ready Django REST Framework APIs. It generates a fully dockerized project with authentication, user accounts, tests, docs, and CI pre-wired. The output is a deployable REST API with best practices baked in — the template itself is what lives in this repo.

## Tech Stack
- **Language:** Python 3.13+
- **Framework:** Django 5.0+ / Django REST Framework
- **Database:** PostgreSQL 16.4+
- **Containers:** Docker + docker-compose
- **Docs:** MkDocs
- **CI:** GitHub Actions (`.github/workflows/push.yaml`)
- **Dependency automation:** pyup (`.pyup.yml`)
- **Packaging:** `pyproject.toml`

## Directory Structure

cookiecutter.json                          # Template variables (inputs)
{{cookiecutter.github_repository_name}}/   # Generated project root
  {{cookiecutter.app_name}}/               # Django app package
    config/                                # Settings: common.py, local.py, production.py
    users/                                 # User model, views, serializers, permissions, tests
    urls.py                                # Root URL config
    wsgi.py                                # WSGI entrypoint
  docs/                                    # MkDocs source (api/, index.md)
  docker-compose.yml                       # Local dev stack
  manage.py                                # Django CLI
  wait_for_postgres.py                     # DB readiness probe
.daemon/                                   # Daemon agent config and specs
.github/workflows/                         # CI pipeline


## How to Run
- **Build:** `docker-compose build`
- **Dev server:** `docker-compose up`
- **Tests:** `docker-compose run --rm web pytest`
- **Generate project from template:** `cookiecutter gh:agconti/cookiecutter-django-rest`

## Key Patterns
- All settings inherit from `config/common.py`; override in `local.py` or `production.py`
- User factories live in `users/test/factories.py` — use factory_boy for test data
- Every new app/resource must include: model, serializer, view, URL registration, test, and docs entry
- Migrations live inside each app under `migrations/`
- Template variables are defined in `cookiecutter.json` — add new inputs there first

## Important Locations
- **Config/settings:** `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/config/`
- **Routes:** `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/urls.py`
- **User model/auth:** `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/users/`
- **CI pipeline:** `.github/workflows/push.yaml`
- **Template inputs:** `cookiecutter.json`
- **Daemon specs:** `.daemon/specs/`
