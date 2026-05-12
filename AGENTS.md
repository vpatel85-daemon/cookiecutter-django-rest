# AGENTS.md

## What This Project Does
cookiecutter-django-rest is a Cookiecutter template that scaffolds production-ready Django REST Framework APIs. It generates a fully dockerized project with authentication, user accounts, tests, docs, and CI baked in. Output is a deployable, scalable REST API — developers add their own resources and ship.

## Tech Stack
- **Language:** Python 3.13+
- **Framework:** Django 5.0+ with Django REST Framework
- **Database:** PostgreSQL 16.4+
- **Containerization:** Docker + docker-compose
- **Docs:** MkDocs
- **CI:** GitHub Actions (`.github/workflows/push.yaml`)
- **Dependency automation:** pyup (`.pyup.yml`)
- **Testing:** pytest (via `pyproject.toml`)

## Directory Structure

cookiecutter.json                            # Template input variables
pyproject.toml                               # Project deps and tooling config
{{cookiecutter.github_repository_name}}/     # Generated project root
  docker-compose.yml                         # Local dev orchestration
  manage.py                                  # Django entrypoint
  conftest.py                                # Pytest root config
  wait_for_postgres.py                       # DB readiness helper
  {{cookiecutter.app_name}}/
    config/                                  # Django settings: common, local, production
    urls.py                                  # Root URL routing
    wsgi.py                                  # WSGI entrypoint
    users/                                   # Auth + user resource
      models.py                              # User model
      views.py                               # User API views
      serializers.py                         # DRF serializers
      permissions.py                         # Custom DRF permissions
      admin.py                               # Django admin registration
      migrations/                            # DB migrations
      test/                                  # Unit + integration tests
        factories.py                         # factory_boy model factories
  docs/api/                                  # Markdown API docs (MkDocs)
.daemon/                                     # Daemon AI agent config
.github/workflows/                           # CI pipelines


## How to Run
- **Build:** `docker-compose up --build`
- **Tests:** `docker-compose run web pytest`
- **Dev server:** `docker-compose up`
- **Linting/formatting:** check `pyproject.toml` for configured tools

## Key Patterns
- All new resources follow the `users/` structure: `models.py`, `views.py`, `serializers.py`, `permissions.py`, `test/`, `migrations/`
- Settings are split: `common.py` (shared), `local.py` (dev overrides), `production.py` (prod overrides)
- Tests use pytest + factory_boy factories — no raw `User.objects.create()` in tests
- Every new endpoint needs a corresponding Markdown doc under `docs/api/`
- Migrations must be generated and committed with model changes

## Where Important Things Live
- **Settings:** `{{cookiecutter.app_name}}/config/`
- **URL routing:** `{{cookiecutter.app_name}}/urls.py`
- **DB schema:** `{{cookiecutter.app_name}}/users/migrations/`
- **CI pipeline:** `.github/workflows/push.yaml`
- **Template variables:** `cookiecutter.json`
- **Daemon config:** `.daemon/`
