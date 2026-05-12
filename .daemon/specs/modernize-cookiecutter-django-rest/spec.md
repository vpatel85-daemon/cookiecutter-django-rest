# Specification

## Who Benefits
Django developers who use this template to bootstrap new REST API projects. They get a modern, well-maintained starting point that follows current best practices.

## What "Done" Looks Like
A freshly generated project from this template runs cleanly on Python 3.13 + Django 5.x, passes all CI checks, uses ruff for linting/formatting, has up-to-date pinned dependencies, and has modernized GitHub Actions workflows.

## Scope
1. **Dependency updates** — update all packages in requirements files to latest compatible versions
2. **Linting/formatting** — replace flake8 + isort + black with ruff (single tool)
3. **CI modernization** — update GitHub Actions workflows to use latest action versions, add Python 3.13 matrix
4. **Django/DRF modernization** — adopt any new patterns from Django 5.x and DRF (e.g. new settings, deprecated removals)
5. **Docs** — update MkDocs config and content to reflect changes
6. **Template hygiene** — clean up any outdated cookiecutter options or defaults
