# Technical Plan

## Architecture
This is a cookiecutter template repo. All changes happen in two layers:
1. **Root level** — `cookiecutter.json`, `hooks/`, root CI workflows, root docs
2. **Template level** — `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/` and surrounding files

## Approach

### Phase 1: Dependency Updates
- Update `requirements/base.txt`, `requirements/local.txt`, `requirements/production.txt` inside the template
- Pin to latest compatible versions for Python 3.13 + Django 5.x
- Remove deprecated packages, add replacements where needed

### Phase 2: Linting Modernization
- Remove `flake8`, `isort`, `black` from requirements
- Add `ruff` with a `ruff.toml` or `pyproject.toml` config inside the template
- Update `Makefile` lint/format targets
- Update `.pre-commit-config.yaml` to use ruff hooks

### Phase 3: CI/CD Modernization
- Update `.github/workflows/` — bump action versions (`actions/checkout@v4`, `actions/setup-python@v5`)
- Add Python 3.13 to test matrix, drop EOL versions if any
- Ensure Docker-based CI steps still work

### Phase 4: Django/DRF Modernization
- Update `MIDDLEWARE`, `INSTALLED_APPS`, and settings for Django 5.x compatibility
- Remove any deprecated DRF patterns or settings
- Update URL patterns if needed (no more `url()`)

### Phase 5: Docs & Template Hygiene
- Update `mkdocs.yml` and docs content
- Review `cookiecutter.json` options — remove stale ones, add useful new ones
- Update README with new setup instructions

## Key Files
- `{{cookiecutter.github_repository_name}}/requirements/`
- `{{cookiecutter.github_repository_name}}/.github/workflows/`
- `{{cookiecutter.github_repository_name}}/{{cookiecutter.app_name}}/settings/`
- `{{cookiecutter.github_repository_name}}/Makefile`
- `{{cookiecutter.github_repository_name}}/.pre-commit-config.yaml`
- `cookiecutter.json`
- `docs/`
