# AGENTS.md

## What This Project Does
cookiecutter-django-rest is a Cookiecutter template that scaffolds production-ready Django REST Framework APIs. It generates authentication, user accounts, tests, docs, and Docker-based local dev in seconds. The output project is deployable, scalable, and follows best practices out of the box.

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

cookiecutter.json                           # Template variables (app_name, repo name, etc.)
pyproject.toml                              # Template-level tooling config
{{cookiecutter.github_repository_name}}/    # Generated project root
  {{cookiecutter.app_name}}/                # Django app package
    config/                                 # Django settings: common.py, local.py, production.py
    users/                                  # User model, serializers, views, permissions
      migrations/                           # DB migrations
      test/                                 # factories.py, test_views.py, test_serializers.py
    urls.py                                 # Root URL config
    wsgi.py                                 # WSGI entry point
  docs/api/                                 # API docs (authentication.md, users.md)
  docker-compose.yml                        # Local dev services
  conftest.py                               # pytest config
  manage.py                                 # Django management entry point
.daemon/                                    # Daemon agent config and specs
.github/workflows/push.yaml                 # CI pipeline


## How to Run
bash
# Install cookiecutter and generate a project
pip install cookiecutter
cookiecutter https://github.com/agconti/cookiecutter-django-rest

# Inside the generated project:
docker-compose up --build        # Start dev server + PostgreSQL
docker-compose run web pytest    # Run tests


## Key Patterns
- All new Django apps follow the `users/` pattern: model → serializer → view → urls → tests → factory
- Settings are split: `common.py` (base), `local.py` (dev overrides), `production.py` (prod overrides)
- Tests use `factory_boy` factories defined in `test/factories.py`; never use raw model creation in tests
- Template files use `{{cookiecutter.*}}` Jinja2 syntax — preserve this in any template-layer edits
- Cookiecutter variables are defined in `cookiecutter.json` — add new template inputs there first

## Where Important Things Live
- **Settings:** `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/config/`
- **Routes:** `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/urls.py`
- **User model/auth:** `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/users/`
- **CI config:** `.github/workflows/push.yaml`
- **Template variables:** `cookiecutter.json`
- **Daemon specs:** `.daemon/specs/`
