# AGENTS.md

Guidance for future agents working in this repository.

## Repository Purpose

This is a Python arena: a ready-to-go scratchpad for trying ideas in a small,
fully bootstrapped Python project. Keep changes lightweight and sympathetic to
that purpose. Do not turn the repository into a large application framework
unless the user explicitly asks for that.

## Project Shape

- Python package code lives under `src/arena/`.
- Tests live under `tests/`.
- The command-line entry point is `arena = "arena.__main__:main"`.
- Development helpers live under `dev/bin/`.
- Dependency and tool configuration lives in `pyproject.toml`.
- The project uses `uv`; prefer `uv` commands over direct `python`, `pip`, or
  tool invocations.

## Validation

Use `dev/bin/check` as the source of truth before considering code changes done.
It currently runs:

```sh
uv lock --check
uv run black --check src tests
uv run isort --check src tests
uv run flake8 src tests
uv run mypy src tests
uv run pytest tests
```

For formatting-only fixes, run:

```sh
dev/bin/autofmt
```

If you only change documentation, it is acceptable to skip the full check, but
say so in your final response.

## Coding Conventions

- Target Python 3.10 or newer.
- Prefer the lowest supported Python version that has a binary available on the
  machine. For example, use `uv sync --python python3.10` when `python3.10` is
  available.
- Keep code typed; mypy is configured with `strict = true`.
- Use `from __future__ import annotations` in Python modules, matching the
  existing files.
- Follow Black formatting with 120-character lines.
- Follow isort using the Black profile.
- Keep tests small and close to the behavior being added or changed.
- Avoid broad abstractions in this arena unless they directly help the
  experiment at hand.

## Working Style

- Read the existing files before editing; this repository is intentionally
  small, so local context should guide the change.
- Prefer focused edits over repo-wide churn.
- Preserve user changes in the working tree. Do not revert or overwrite work you
  did not make unless the user explicitly requests it.
- When adding dependencies, update `pyproject.toml` through `uv` where possible
  and make sure `uv.lock` remains consistent.
- Keep generated artifacts, caches, and virtual environments out of commits.
