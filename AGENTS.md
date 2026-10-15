# AGENTS.md — working rules

Rules for anyone (human or agent) working in this repository.

## 1. Read these first, in order

1. `README.md` — what this project is and how to run it
2. `PLAN.md` — where the work stands and what comes next

Do not start implementation before both have been read. If what you find
contradicts the task you were given, stop and say so rather than picking one.

## 2. Python: use uv, always

All Python runs through [uv](https://docs.astral.sh/uv/). There is no global
environment to install into.

| Do | Do not |
|---|---|
| `uv run <script-or-command>` | `python <script>`, bare `pip install` |
| `uv add <package>` | `pip install <package>` (global) |
| `uv add --dev <package>` | `pip install --user <package>` |
| `uv lock` / `uv sync` | `virtualenv`, `python -m venv` by hand |
| `uvx <tool>` for one-offs | `pipx install`, global tool installs |

Dependencies belong in `pyproject.toml` (managed by `uv add`), pinned in
`uv.lock`. If you find yourself editing a `requirements.txt` or activating a
virtualenv, you are off-path.

Never install into the system Python. If a `pip install` is genuinely the only
route, say why and get agreement first.

## 3. Run checks before saying it is done

"Done" means a check was run and you read its output. Before reporting
completion:

1. **Run the relevant check** — tests, lint, type check, or for a script, an
   actual execution that exercises the change.
2. **Read the output.** Do not report success on an exit code alone if the
   output contradicts it.
3. **Paste the relevant output** in your report, including failures.

If no check exists for what you changed, say that explicitly — an unverified
change is a known gap, not a pass. If a check fails, report the failure with
its output; never soften, never skip, and never describe skipped work as
finished.

Fix a broken check rather than working around it. Suppressing the check is a
change in behaviour and must be called out.

## 4. Keeping the docs honest

- `PLAN.md` — update progress and the next step when you finish or learn something.
- `RUNS.md` — append an entry for each requested change: the model used, what
  was asked, and how it was verified. Newest at the top.
- `README.md` — update when how-you-run-things changes.

Stale docs are worse than missing ones: if you notice a file that no longer
matches the code, fix it in the same change or flag it.
