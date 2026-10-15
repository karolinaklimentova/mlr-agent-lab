# PLAN.md

Progress and the next step. Update this file as work lands.

## Status

Bootstrapping. The repo exists and has working rules, but no real code yet.

## Done

- [x] Repo initialised on `main`; published as a public GitHub repo
      (`karolinaklimentova/mlr-agent-lab`), `hello.py` pushed.
- [x] Toolchain in place, user-level (no admin rights): `gh` 2.102.0,
      `uv` / `uvx` 0.13.1 in `~/.local/bin`.
- [x] Working rules written: `AGENTS.md`, loaded via `CLAUDE.md`.
- [x] `README.md` (goal + how to run), `PLAN.md`, `RUNS.md` created.
- [x] Verified `uv run hello.py` prints `hello`.

## Next step

**Create the uv project manifest** so dependencies can be tracked:

```bash
uv init --bare --name mlr-agent-lab .   # or: uv add <first dependency>
uv add --dev pytest ruff mypy
uv run pytest
```

This makes `uv add` and `uv sync` work — both currently fail because there is
no `pyproject.toml`.

## After that

- [ ] Define what the first MLR agent experiment actually is (currently undefined —
      the goal in `README.md` is a placeholder).
- [ ] Add a real check: tests under `tests/`, `ruff` and `mypy` configured in
      `pyproject.toml`, so "run checks before done" has something to run.
- [ ] Consider a `Makefile` or task runner so checks are one command.

## Open questions

- What does MLR stand for here in practice, and what is the first task the
  agent should complete?
- Should this stay public while it is exploratory?
- `/Users/karolinaklimentova/.git` is a stray repo (0 tracked files, no
  commits) that shadows this one when working from the home directory. Decide
  whether to delete it.
