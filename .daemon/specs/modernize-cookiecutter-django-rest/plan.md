# Technical Plan

## Architecture
This is a cookiecutter template repo. All changes touch files inside:
- `{{cookiecutter.github_repository_name}}/` — the generated project root
- `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/` — the Django app
- `cookiecutter.json` — template variables
- `hooks/` — pre/post generation hooks
- `.github/workflows/` — CI for the template repo itself

## Approach

### 1. Dependency management → uv + pyproject.toml
- Remove `requirements/` directory (base.txt, local.txt, production.txt)
- Add `pyproject.toml` with `[project]` and `[tool.uv]` sections
- Update `Dockerfile` to install `uv` and use `uv sync` instead of `pip install -r`
- Update `docker-compose.yml` references accordingly

### 2. Python & Django version bump
- Pin Python to 3.13 in `Dockerfile` and `.python-version`
- Upgrade Django to 5.x, DRF to latest, all other deps to latest stable

### 3. Linting/formatting → ruff
- Remove flake8, isort, black config files (`.flake8`, `setup.cfg` linting sections)
- Add `ruff` to dev dependencies with `pyproject.toml` config
- Update pre-commit config if present

### 4. GitHub Actions CI modernization
- Bump all action versions (`actions/checkout@v4`, `actions/setup-python@v5`, etc.)
- Replace pip-tools steps with uv equivalents
- Ensure matrix covers Python 3.13

### 5. Docker / docker-compose
- Use `docker-compose.yml` v3.9+ syntax (or drop version key per current spec)
- Use multi-stage build in Dockerfile where appropriate

### 6. MkDocs
- Bump `mkdocs` and `mkdocs-material` to latest
- Fix any broken doc references

### 7. Bug fixes & cleanup
- Fix any broken template references found during the above work
- Remove dead code / unused files
