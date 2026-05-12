# Project Memory

## Stack
- Cookiecutter template → outputs Django 5.0+ / DRF / PostgreSQL 16.4+ / Docker projects.
- Tooling: `pyproject.toml` for packaging, `pytest` + `factory_boy` for tests, GitHub Actions for CI, pyup for dependency automation.

## Gotchas
- This is a **template repo**, not a runnable app. Files under `{{cookiecutter.github_repository_name}}/` use Jinja2 `{{cookiecutter.*}}` syntax — never strip or escape those brackets.
- Two layers of config: the template's own `pyproject.toml` (for cookiecutter deps) and the *generated* project's deps inside the template directory — keep them separate.
- `wait_for_postgres.py` is wired into the Docker startup chain — removing it will break generated projects silently.
- Specs for planned work live in `.daemon/specs/` — check there before starting any maintenance or modernization task.

## First cycle: bootstrap complete.
