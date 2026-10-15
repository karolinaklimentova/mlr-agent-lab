# mlr-agent-lab

MLR (machine-learning research) agent lab — experiments with agents that run
research tasks end to end.

> Early stage. See [PLAN.md](PLAN.md) for where this stands.

## Requirements

- [uv](https://docs.astral.sh/uv/) — manages Python and all dependencies
- Python is provided by uv; a system Python is not required

`uv` and `gh` are installed in `~/.local/bin` on the working machine.

## How to run things

```bash
uv run hello.py          # run a script
uv add <package>         # add a runtime dependency
uv add --dev <package>   # add a dev dependency (tests, lint, typing)
uvx <tool>               # run a tool without installing it
uv sync                  # install/set up the project environment
```

`uv run` creates and reuses the project environment automatically — there is no
need to activate a virtualenv or install anything globally.

**Note:** `uv sync` currently fails with *"No `pyproject.toml` found"*. The repo
has no project manifest yet, so `uv run` works (ephemeral environment) but
`uv add`/`uv sync` need one first. Creating it is the next step in
[PLAN.md](PLAN.md).

## Layout

| Path | What it is |
|---|---|
| `hello.py` | Smoke-test script: prints `hello` |
| `AGENTS.md` | Working rules for humans and agents |
| `CLAUDE.md` | Loads `AGENTS.md` into Claude Code |
| `PLAN.md` | Progress and the next step |
| `RUNS.md` | Log of requested changes and how each was verified |

## Checks

```bash
uv run hello.py
```

Prints `hello` and exits 0. No test suite yet — see [PLAN.md](PLAN.md).

## Working rules

Read [AGENTS.md](AGENTS.md) first. Short version: read `README.md` and
`PLAN.md` before starting, use `uv` for all Python, and run checks before
claiming anything is done.
