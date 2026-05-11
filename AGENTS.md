# AGENTS.md

## What This Project Does
cookiecutter-django-rest is a Cookiecutter template that scaffolds production-ready Django REST Framework APIs. It generates a fully dockerized project with authentication, user accounts, tests, and CI out of the box. The goal is to eliminate boilerplate so developers can immediately focus on domain logic.

## Tech Stack
- **Language**: Python 3.13+
- **Framework**: Django 5.0+ with Django REST Framework
- **Database**: PostgreSQL 16.4+
- **Containerization**: Docker + docker-compose
- **Testing**: pytest (conftest.py at project root)
- **Docs**: MkDocs (mkdocs.yml)
- **Template Engine**: Cookiecutter (cookiecutter.json defines template variables)

## Directory Structure

cookiecutter.json                        # Template input variables (app_name, github_repository_name, etc.)
{{cookiecutter.github_repository_name}}/ # The generated project root
  {{cookiecutter.app_name}}/             # Django app package
    config/                              # Django settings: common.py, local.py, production.py
    users/                               # Built-in users app: models, views, serializers, permissions
      migrations/                        # DB migrations
      test/                              # Tests: factories.py, test_views.py, test_serializers.py
    urls.py                              # Root URL configuration
    wsgi.py                              # WSGI entry point
  docs/                                  # MkDocs API documentation
  docker-compose.yml                     # Local dev services (app + postgres)
  manage.py                              # Django management entry point
  wait_for_postgres.py                   # DB readiness helper
.github/workflows/push.yaml              # CI pipeline


## How To Run
bash
# Build and start local dev environment
docker-compose up --build

# Run tests (inside container or with local venv)
pytest

# Apply migrations
python manage.py migrate


## Key Patterns
- All new Django apps follow the `users/` structure: `models.py`, `views.py`, `serializers.py`, `permissions.py`, `admin.py`, `migrations/`, `test/`
- Tests use `factories.py` (factory_boy) for object creation — never raw model instantiation in tests
- Settings are split by environment: extend `common.py` in `local.py` / `production.py`, never modify common directly for env-specific values
- Cookiecutter variables (`{{cookiecutter.app_name}}`) appear in file/folder names and inside file contents — preserve this convention for any template-level changes

## Important Locations
- **Config/Settings**: `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/config/`
- **URL Routes**: `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/urls.py`
- **DB Schema**: migrations in each app's `migrations/` directory
- **Template variables**: `cookiecutter.json`
- **CI**: `.github/workflows/push.yaml`
