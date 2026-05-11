# Principles: Maintenance & Dependency Updates

## Non-negotiables
- Upgrade all dependencies to latest stable major versions (Django 5.x, DRF, Celery, etc.)
- Fix or update any tests that break as a result of upgrades
- Do not leave the project in a broken state — all tests must pass at the end
- Prefer dropping deprecated patterns over keeping backward-compat shims

## Guiding values
- Latest stable > safe but outdated
- Clean breaks over messy compatibility layers
- Tests are the safety net — keep them green
