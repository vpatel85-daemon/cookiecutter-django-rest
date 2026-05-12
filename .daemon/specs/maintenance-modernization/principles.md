# Principles

- Target latest stable versions: Python 3.12, Django 5.1, DRF 3.15
- One tool where possible: Ruff replaces flake8 + isort + black
- Keep it a valid cookiecutter template throughout — no template variables broken
- CI must pass after all changes
- Docker images pinned to specific modern versions, not `latest` tags
- No deprecated Django patterns in generated code
