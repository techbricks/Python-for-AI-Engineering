# Python for AI Engineering

Course notebooks, grouped by module.

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
