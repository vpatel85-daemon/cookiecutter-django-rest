# Principles

## Non-Negotiables
- Keep the project as a cookiecutter template — the generated project must be functional out of the box
- All changes must be backward-compatible with the template rendering system (Jinja2 `{{cookiecutter.*}}` variables)
- No breaking changes to the generated project's public API or structure without versioning

## Goals
- Modernize tooling: replace flake8/isort/black with ruff, update CI workflows
- Update all dependencies to latest compatible versions (Python 3.13+, Django 5.x, DRF latest)
- Improve developer experience: better docs, cleaner defaults, modern patterns
- Maintain stability: all changes are tested and verified before merging
