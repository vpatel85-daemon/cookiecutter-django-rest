# Technical Plan: Maintenance & Dependency Updates

## Approach
Work in dependency layers — upgrade the core runtime first (Python, Django), then the ecosystem (DRF, Celery), then dev tooling. Run tests at each layer boundary so failures are isolated and attributable.

## Upgrade order
1. Python 3.12 base image + Docker updates
2. Django 5.x — biggest surface area, do first
3. Django REST Framework latest — depends on Django version
4. Celery + redis/kombu to latest
5. All remaining requirements (prod + dev)
6. Tooling: replace flake8/isort/black with ruff, update pre-commit config
7. GitHub Actions: pin all actions to latest major versions
8. Test suite: fix any failures introduced by the above

## Files in scope
- `requirements/*.txt` (base, local, production, test)
- `Dockerfile` / `docker-compose.yml`
- `.pre-commit-config.yaml`
- `.github/workflows/*.yml`
- `setup.cfg` / `pyproject.toml` (linting config)
- Any test files that break
