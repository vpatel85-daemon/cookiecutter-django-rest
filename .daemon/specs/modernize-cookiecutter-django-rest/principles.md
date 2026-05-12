# Principles

## Non-negotiables
- Modernize the cookiecutter-django-rest template to reflect current best practices
- Migrate dependency management to `uv` (replacing pip-tools)
- Keep backward compatibility in spirit: generated projects must still work out-of-the-box with Docker + PostgreSQL
- No breaking changes to the template's public interface (cookiecutter.json variables stay stable unless there's a strong reason)
- All changes must leave the CI (GitHub Actions) green
- Prefer incremental, reviewable PRs over large sweeping rewrites
