# Specification

## Goal
Modernize the cookiecutter-django-rest template so that any developer who generates a new project gets a batteries-included, production-ready Django REST API with current tooling, best practices, and zero cruft to clean up.

## Done means
- `cookiecutter` generates a project that installs cleanly with `uv`, passes `ruff` + `mypy`, runs tests via GitHub Actions matrix (Python 3.12/3.13, Django 5.0/5.1), and ships with JWT auth + OpenAPI schema out of the box.

## Users
Django developers starting a new REST API project who want a modern, opinionated starting point.

## Out of scope
- Frontend scaffolding
- Deployment automation (Render, Heroku, etc.)
- Celery / async task queue setup
