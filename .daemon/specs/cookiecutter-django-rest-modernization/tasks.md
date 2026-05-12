# Tasks

## Epic: Dependency Modernization

### Task: Update cookiecutter.json defaults
Description: Update `cookiecutter.json` to default to Python 3.13 and Django 5.1. Review all default values for accuracy and remove any stale options.
Acceptance criteria:
- `cookiecutter.json` references Python 3.13 and Django 5.1 as defaults
- All options are current and documented
Depends on:

### Task: Bump requirements to latest stable
Description: Read all files under `{{cookiecutter.github_repository_name}}/requirements/` (base.txt, local.txt, production.txt) and bump every package to its latest stable version. Ensure Django 5.1+, DRF 3.15+, and all supporting packages are current.
Acceptance criteria:
- All packages pinned to latest stable
- No known CVEs in pinned versions
- Requirements files are clean and well-commented
Depends on: Update cookiecutter.json defaults

### Task: Add uv support
Description: Add `uv` as the recommended package manager. Create or update `pyproject.toml` inside the template with `[project]` metadata and a `uv.lock` generation step. Update any install instructions in the Makefile and README to use `uv sync` instead of `pip install -r`.
Acceptance criteria:
- `pyproject.toml` exists with correct metadata inside the template
- `make install` uses `uv sync`
- README install instructions updated
Depends on: Bump requirements to latest stable

## Epic: Code Quality & Linting

### Task: Replace flake8/isort/black with ruff
Description: Remove `.flake8`, `setup.cfg` linting config, and any black/isort config. Add `ruff` configuration to `pyproject.toml` with rules equivalent to the previous setup (E, F, I, UP, B). Ensure `ruff format` replaces black.
Acceptance criteria:
- `ruff check .` and `ruff format .` pass on the template source
- No flake8/black/isort config files remain
- `pyproject.toml` contains `[tool.ruff]` section
Depends on: Add uv support

### Task: Add mypy and django-stubs
Description: Add `mypy` and `django-stubs` to dev dependencies. Create `mypy.ini` or `[tool.mypy]` config in `pyproject.toml` with Django plugin enabled. Fix any type errors surfaced in the template app code.
Acceptance criteria:
- `mypy .` runs without errors on template source
- `django-stubs` is in dev requirements
- Config is in `pyproject.toml`
Depends on: Replace flake8/isort/black with ruff

### Task: Update pre-commit hooks
Description: Rewrite `.pre-commit-config.yaml` to use ruff (check + format) and mypy hooks. Remove hooks for flake8, black, isort. Pin all hook versions to latest.
Acceptance criteria:
- `pre-commit run --all-files` passes
- Only ruff and mypy hooks present for linting
- Hook versions are pinned
Depends on: Add mypy and django-stubs

## Epic: CI/CD Modernization

### Task: Rewrite GitHub Actions CI workflow
Description: Rewrite `.github/workflows/` CI to use `uv` for installs, and add a matrix over Python 3.12 + 3.13 and Django 5.0 + 5.1. Pin all `uses:` action versions to latest. Run ruff, mypy, and pytest in CI.
Acceptance criteria:
- CI matrix covers Python 3.12/3.13 × Django 5.0/5.1
- Uses `uv` for dependency install
- ruff, mypy, and pytest all run as separate steps
- All action versions are pinned
Depends on: Update pre-commit hooks

### Task: Add cookiecutter generation smoke test
Description: Add a CI job that runs `cookiecutter . --no-input` and then runs the generated project's tests. This validates that the template itself generates a working project.
Acceptance criteria:
- CI job generates a project from the template with default values
- Generated project installs and tests pass
- Job runs on every PR and push to main
Depends on: Rewrite GitHub Actions CI workflow

## Epic: Django/DRF Best Practices

### Task: Audit and modernize settings split
Description: Review `config/settings/common.py`, `local.py`, and `production.py` inside the template. Ensure SECRET_KEY uses env var with no default, ALLOWED_HOSTS is env-driven in production, DATABASE_URL is used via `dj-database-url`, and INSTALLED_APPS is clean.
Acceptance criteria:
- No hardcoded secrets in any settings file
- `dj-database-url` used for DB config
- Production settings are safe by default
- `django.contrib.staticfiles` and other defaults are correctly configured
Depends on: Rewrite GitHub Actions CI workflow

### Task: Add drf-spectacular for OpenAPI schema
Description: Add `drf-spectacular` to requirements. Configure it in settings (`REST_FRAMEWORK` `DEFAULT_SCHEMA_CLASS`). Add `/api/schema/`, `/api/schema/swagger-ui/`, and `/api/schema/redoc/` URLs to the template's URL config.
Acceptance criteria:
- `drf-spectacular` in base requirements
- Schema endpoint returns valid OpenAPI 3.1 JSON
- Swagger UI and ReDoc endpoints work
- Settings configured correctly
Depends on: Audit and modernize settings split

### Task: Add djangorestframework-simplejwt
Description: Add `djangorestframework-simplejwt` to requirements. Configure it as the default authentication class in `REST_FRAMEWORK` settings. Add `/api/token/` and `/api/token/refresh/` URL endpoints. Set sensible token lifetimes (access: 15 min, refresh: 7 days).
Acceptance criteria:
- `simplejwt` in base requirements
- Token obtain and refresh endpoints exist and return valid tokens
- `DEFAULT_AUTHENTICATION_CLASSES` set to `JWTAuthentication`
- Token lifetimes configured in settings
Depends on: Add drf-spectacular for OpenAPI schema

## Epic: Developer Experience

### Task: Update docker-compose to Compose v2 syntax
Description: Rewrite `docker-compose.yml` inside the template to use Compose v2 syntax — remove the top-level `version:` key, use `depends_on` with `condition: service_healthy`, and add a healthcheck for the postgres service.
Acceptance criteria:
- No `version:` key in docker-compose.yml
- Postgres service has a healthcheck
- App service uses `depends_on` with health condition
- `docker compose up` starts successfully
Depends on: Add djangorestframework-simplejwt

### Task: Improve Makefile with standard dev commands
Description: Add or rewrite the `Makefile` inside the template with commands: `make install` (uv sync), `make run` (docker compose up), `make test` (pytest), `make lint` (ruff check + mypy), `make migrate`, `make shell`.
Acceptance criteria:
- All 6 commands present and functional
- Commands use `uv run` where appropriate
- Makefile has a `help` target listing all commands
Depends on: Update docker-compose to Compose v2 syntax

### Task: Update README and MkDocs documentation
Description: Rewrite the top-level `README.md` and update MkDocs docs to reflect all changes: uv install, ruff/mypy tooling, JWT auth, OpenAPI schema endpoints, updated CI badges, and updated quick-start instructions.
Acceptance criteria:
- README quick-start uses `uv`
- JWT and OpenAPI sections documented
- CI badge reflects new workflow name
- MkDocs pages are accurate and build without errors
Depends on: Improve Makefile with standard dev commands
