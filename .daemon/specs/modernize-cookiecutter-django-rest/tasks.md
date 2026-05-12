# Tasks

## Epic: Dependency Updates

### Task: Audit and update base dependencies
Description: Read `requirements/base.txt` in the template directory. Update Django to 5.x, DRF to latest, and all other packages to their latest compatible versions. Remove any packages that are no longer needed or have been superseded.
Acceptance criteria:
- All packages in `requirements/base.txt` are at their latest compatible versions
- No deprecated or abandoned packages remain
- File is cleanly formatted with pinned versions
Depends on:

### Task: Audit and update local/dev dependencies
Description: Read `requirements/local.txt` in the template directory. Update all dev/test packages (pytest, coverage, factory-boy, etc.) to latest compatible versions.
Acceptance criteria:
- All packages in `requirements/local.txt` are at latest compatible versions
- No conflicts with base requirements
Depends on: Audit and update base dependencies

### Task: Audit and update production dependencies
Description: Read `requirements/production.txt` in the template directory. Update gunicorn, sentry-sdk, whitenoise, and other production packages to latest versions.
Acceptance criteria:
- All packages in `requirements/production.txt` are at latest compatible versions
Depends on: Audit and update base dependencies

## Epic: Linting and Formatting Modernization

### Task: Replace flake8/isort/black with ruff
Description: Remove `flake8`, `isort`, and `black` from `requirements/local.txt`. Add `ruff` at its latest version. Create a `ruff.toml` (or add `[tool.ruff]` section to `pyproject.toml`) inside the template with sensible defaults matching the previous config. Update `Makefile` lint and format targets to use `ruff check` and `ruff format`.
Acceptance criteria:
- `flake8`, `isort`, `black` removed from requirements
- `ruff` added and configured
- `make lint` and `make format` work with ruff
- Ruff config covers line length, import sorting, and common rule sets (E, F, I, UP)
Depends on: Audit and update local/dev dependencies

### Task: Update pre-commit config to use ruff
Description: Update `.pre-commit-config.yaml` inside the template to replace flake8/isort/black hooks with ruff and ruff-format hooks from `https://github.com/astral-sh/ruff-pre-commit`.
Acceptance criteria:
- `.pre-commit-config.yaml` uses ruff hooks only (no flake8/isort/black)
- Hook versions are pinned to latest ruff release
Depends on: Replace flake8/isort/black with ruff

## Epic: CI/CD Modernization

### Task: Update GitHub Actions workflow versions
Description: Read all workflow files in `.github/workflows/` inside the template. Bump `actions/checkout` to v4, `actions/setup-python` to v5, and any other outdated action versions. Ensure workflow syntax is current.
Acceptance criteria:
- All GitHub Actions use latest major versions
- No deprecation warnings in workflow files
Depends on:

### Task: Update Python version matrix in CI
Description: Update the CI workflow to test against Python 3.11, 3.12, and 3.13. Remove any EOL Python versions (3.9 and below). Update the `python-version` matrix entries.
Acceptance criteria:
- CI matrix includes Python 3.11, 3.12, 3.13
- EOL versions removed
- All matrix jobs pass
Depends on: Update GitHub Actions workflow versions

### Task: Update Docker base images
Description: Review `Dockerfile` and `docker-compose.yml` in the template. Update Python base image to `python:3.13-slim` and PostgreSQL image to `postgres:16`. Ensure all services start correctly.
Acceptance criteria:
- Dockerfile uses `python:3.13-slim`
- docker-compose uses `postgres:16`
- `docker-compose up` starts without errors
Depends on: Audit and update base dependencies

## Epic: Django and DRF Modernization

### Task: Update settings for Django 5.x compatibility
Description: Read the settings files (`common.py`, `local.py`, `production.py`) in the template. Remove any deprecated settings, add new required settings for Django 5.x (e.g. `STORAGES`, updated `DEFAULT_AUTO_FIELD`, etc.). Check for any middleware or app ordering changes.
Acceptance criteria:
- No Django deprecation warnings on startup
- Settings follow Django 5.x conventions
- `DEFAULT_AUTO_FIELD = "django.db.models.BigAutoField"` set
Depends on: Audit and update base dependencies

### Task: Remove deprecated DRF patterns
Description: Review DRF-related code in the template (views, serializers, routers, settings). Remove any deprecated patterns — e.g. old renderer classes, deprecated settings keys like `DEFAULT_AUTHENTICATION_CLASSES` format changes.
Acceptance criteria:
- No DRF deprecation warnings
- All DRF settings use current key names
- Serializer and view patterns follow current DRF best practices
Depends on: Update settings for Django 5.x compatibility

## Epic: Docs and Template Hygiene

### Task: Update MkDocs config and dependencies
Description: Update `mkdocs.yml` at the repo root and in the template. Bump `mkdocs` and `mkdocs-material` to latest versions in docs requirements. Update any deprecated config keys.
Acceptance criteria:
- `mkdocs build` runs without warnings
- Docs dependencies are at latest versions
Depends on:

### Task: Refresh README and docs content
Description: Update the root `README.md` and `docs/` content to reflect all the changes made — new Python/Django versions, ruff instead of flake8/black, updated setup instructions.
Acceptance criteria:
- README shows correct Python/Django version requirements
- Setup instructions are accurate and work end-to-end
- Ruff mentioned instead of flake8/black
Depends on: Replace flake8/isort/black with ruff, Update MkDocs config and dependencies

### Task: Review and update cookiecutter.json
Description: Read `cookiecutter.json` at the repo root. Remove any stale options, update default values (e.g. default Python version, default Django version). Add any new useful options that reflect the modernized template.
Acceptance criteria:
- `cookiecutter.json` has clean, current defaults
- No stale or unused template variables
- Default Python version is 3.13
Depends on: Update settings for Django 5.x compatibility
