# Specification

## Goal
Modernize cookiecutter-django-rest so that teams bootstrapping a new Django REST API get a template that uses current tooling, up-to-date dependencies, and clean project structure — without having to immediately fix or upgrade anything themselves.

## Who benefits
Developers starting a new Django REST project who want a production-ready, low-maintenance starting point.

## "Done" looks like
- Generated projects use `uv` for dependency management with `pyproject.toml`
- Django, DRF, and all supporting packages are on their latest stable versions
- Python version is 3.13+
- GitHub Actions CI uses modern action versions and passes on first run
- Docker / docker-compose config is current and functional
- MkDocs documentation config is up to date
- Code style tooling (ruff or equivalent) replaces any legacy flake8/black setup
- No known bugs or broken references in the template
