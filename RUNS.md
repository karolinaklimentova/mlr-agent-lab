# RUNS.md

Log of requested changes and how each was verified. Newest entry first.

Each entry records: the model from `/status`, what was asked, and how it was
checked.

> **Model field caveat.** The agent cannot run `/status` itself — only you can.
> Entries below record what the agent could read from its own environment
> (`ANTHROPIC_MODEL` and the CLI version). `/status` is authoritative; correct
> the entry if it disagrees.

---

## 2026-10-15 — Working rules + project docs

- **Model:** `/status` value not captured by the agent. Environment reported
  `ANTHROPIC_MODEL=agentic` via gateway `llm.ai.e-infra.cz`, effort `high`,
  Claude Code CLI `2.1.300`.
- **Asked:** Write `AGENTS.md` with working rules (read `README.md` + `PLAN.md`
  first; use uv for Python — `uv run`, `uv add`, no global pip install; run
  checks before saying done). Make `CLAUDE.md` load it. Create `README.md`
  (goal, how to run), `PLAN.md` (progress, next step), `RUNS.md` (model from
  `/status`, what was asked, how it was checked).
- **Files changed:** `AGENTS.md`, `CLAUDE.md`, `README.md`, `PLAN.md`,
  `RUNS.md` — all new.
- **How it was checked:**
  - `claude --version` → `2.1.300`; confirmed it supports `@file` imports, the
    mechanism `CLAUDE.md` uses to load `AGENTS.md`.
  - `uv run hello.py` → printed `hello`, exit 0. This is the command the
    README tells people to run.
  - `uv sync` → **failed**: `No pyproject.toml found`. Rather than leave an
    unverified claim in the README, the command was reordered and the failure
    documented, with the fix queued as the next step in `PLAN.md`.
  - Pre-existing files confirmed absent (`ls`) before writing, so nothing was
    overwritten.
- **Not verified / known gaps:**
  - `CLAUDE.md` auto-loading `AGENTS.md` is not testable from inside this
    session — it takes effect on the next session start. Check by starting a
    fresh session and asking what the working rules are.
  - No `pyproject.toml`, so `uv add` / `uv sync` do not work yet.
  - These files are not committed or pushed.

---

## 2026-10-15 — Create public repo `mlr-agent-lab` and push

- **Model:** `/status` value not captured; same environment as above.
- **Asked:** Use `gh` to create a public GitHub repository called
  `mlr-agent-lab` from this folder. Show what will be uploaded before pushing.
- **How it was checked:**
  - Preview before push: `git status --short`, staged file list with sizes,
    full `cat` of every staged file, plus a grep for credential-shaped strings
    (`ghp_`/`gho_`/`github_pat_`/`sk-`/`AKIA`/private keys/password keywords)
    over the staged diff → clean. 1 file, 15 bytes.
  - Paused for explicit confirmation before making it public.
  - After push, read state back **from GitHub**, not from local git:
    `gh repo view --json visibility,url,defaultBranchRef` →
    `visibility: PUBLIC`, branch `main`.
  - Unauthenticated `curl` of
    `raw.githubusercontent.com/.../main/hello.py` → HTTP 200,
    `print("hello")`, confirming world-readable.
  - `gh api .../git/trees/main?recursive=1` → exactly one blob, `hello.py` 15 B.
- **Not verified / known gaps:** nothing outstanding for this item. Noted that
  `/Users/karolinaklimentova/.git` is a stray repo whose untracked file list
  includes shell history and dotfiles; this folder now has its own `.git`, which
  shadows it.

---

## 2026-10-15 — Install `gh` and `uv` without admin rights

- **Model:** `/status` value not captured; same environment as above.
- **Asked:** Install GitHub CLI (`gh`) and `uv` into the user folder without
  administrator rights, and check both work.
- **How it was checked:**
  - Preflight: `uname -sm` → `Darwin arm64`; confirmed `~/.local/bin` exists,
    is user-writable, and is already on `PATH` via `~/.zshrc`.
  - Installed with `install -m 755` to `~/.local/bin/`; no `sudo`, nothing
    written outside the home directory. Cleared `com.apple.quarantine`.
  - Versions: `gh 2.102.0`, `uv 0.13.1`, `uvx 0.13.1`.
  - PATH persistence checked in a **fresh login shell** (`zsh -l -c`) so the
    result does not depend on this session's exported PATH.
  - Functional test, not just `--version`: `uv venv` created a working 3.12
    virtualenv and executed Python inside it.
- **Not verified / known gaps:** `gh` was installed but unauthenticated at the
  time (`gh api /meta` returned "please run: gh auth login"). The interactive
  login was left to you; a later entry confirms `gh` was authenticated as
  `karolinaklimentova`.

---

## 2026-10-15 — git identity

- **Model:** `/status` value not captured; same environment as above.
- **Asked:** Set the global git name to `karolinaklimentova` and the email to
  `257007@vutbr.cz`.
- **How it was checked:** read config before and after with
  `git config --global --get user.name` / `user.email`. Name changed from
  `Karolina Klimentova`; email was already correct. Later confirmed in practice
  — commit `b876f84` was authored `karolinaklimentova <257007@vutbr.cz>`.

---

## 2026-10-15 — First program

- **Model:** `/status` value not captured; same environment as above.
- **Asked:** Write a Python program that prints hello, and run it.
- **Files changed:** `hello.py` (new, 15 bytes).
- **How it was checked:** `python3 hello.py` → printed `hello`. Re-checked later
  via `uv run hello.py` → `hello`, exit 0.
