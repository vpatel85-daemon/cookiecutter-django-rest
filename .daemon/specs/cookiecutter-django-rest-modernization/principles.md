# Principles

## Non-negotiables
- All changes happen inside the cookiecutter template — paths use `{{cookiecutter.*}}` literal directory names
- Backward compatibility is not required — this is a greenfield template, modernization takes priority
- Every change must result in a working, generatable Django REST project
- Dependencies must be pinned to latest stable (not bleeding edge)
- `uv` replaces `pip` as the package manager throughout

## Priorities (in order)
1. Dependency modernization (requirements, Python/Django version defaults)
2. Code quality tooling (ruff, mypy, pre-commit)
3. CI/CD modernization (GitHub Actions, matrix testing)
4. Django/DRF best practices (settings, OpenAPI, JWT auth)
5. Developer experience (Docker, Makefile, docs)
