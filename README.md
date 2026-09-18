# Python for AI Engineering

Course notebooks, grouped by module. **41 required + 2 optional.**

Start with `module_01/m1-1-mini-env-setup.ipynb` — it walks through IDE, Git, uv, clone, `uv sync`, and `.env` secrets.

**Core path (no paid API key):** mock + hosted adapter against recorded fixtures + CLI.  
**Optional:** `module_06/m6-4-mini-local-backend.ipynb`, `module_10/m10-2-mini-http-endpoint.ipynb`.

## Setup

Install [uv](https://docs.astral.sh/uv/), then from this folder:

```bash
uv lock    # refresh uv.lock if pyproject.toml changed (already committed)
uv sync    # create .venv and install the locked versions
```

`uv sync` is the install step (uv has no project-level `uv install`). It reads `pyproject.toml` + `uv.lock` and installs the same versions the instructor used.

Then in Cursor or VS Code: **Python: Select Interpreter** → `.venv`.

| File | Role |
|------|------|
| `pyproject.toml` | Declares the packages the course notebooks import |
| `uv.lock` | Pins exact versions for a reproducible install |

## Notebooks

| Module | Required notebooks | Optional |
|---|---|---|
| 1 | env-setup, first-win, CSV wall, tracebacks | — |
| 2 | smells→function, typed shapes, package, refactor wall | — |
| 3 | paths, csv/json, pandas, ingest wall | — |
| 4 | pin deps, layout, git init, clone-and-run | — |
| 5 | debug tree, import failures, data failures, broken-repo wall | — |
| 6 | protocol, prompt/parser, hosted, swap wall | local backend |
| 7 | schemas+settings, exceptions+retry, logging, fault-injection wall | — |
| 8 | pytest+fixtures, fake client, bug-log wall | — |
| 9 | baseline+gold set, latency/cost, prompt A/B wall | — |
| 10 | CLI, runtime-debug wall, black-box wall | FastAPI |
| 11 | capstone, docs wall, release audit, wrap-up | — |
