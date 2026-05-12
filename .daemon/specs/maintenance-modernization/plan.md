# Technical Plan

## Approach
Work through the repo in dependency order: runtime first, then framework deps, then tooling, then infrastructure, then docs.

## Epics
1. **Runtime & Dependencies** — Python 3.12, pyproject.toml, all pinned deps bumped
2. **Linting & Formatting** — Ruff replaces flake8/isort/black, pre-commit updated
3. **Docker & Infrastructure** — base images bumped, compose modernized
4. **CI/CD** — GitHub Actions updated to latest actions, Python 3.12 matrix
5. **Code Cleanup** — remove deprecated Django patterns, update settings
6. **Documentation** — README badges, version refs, setup instructions

## Key Files
- `{{cookiecutter.project_slug}}/requirements/` — dep files to bump
- `setup.cfg` / `setup.py` → migrate to `pyproject.toml`
- `.pre-commit-config.yaml` — hook versions
- `.github/workflows/` — CI pipeline
- `docker-compose.yml` + `Dockerfile` — infrastructure
- `README.md` — docs
