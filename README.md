# rdl-python-ambiguous

Test fixture for the `remove_duplicate_lockfiles` maintenance task.

## Scenario

Python conflict at repo root with **no** detection signals — no `pyproject.toml`, no `Pipfile`.

Lockfiles:
- `poetry.lock`
- `uv.lock`

(A `requirements.txt` is present but the MT does not use it for detection.)

## Expected MT behaviour

- **Cannot auto-detect**; issues a `select` question asking which of `poetry` / `uv` to keep.
- Default is `uv` (the ecosystem default in `_DEFAULT_MANAGER` for python).
- Also issues the `update_gitignore` boolean question (default `true`).
- Plan and apply phases delete the non-chosen lockfile and append it to `.gitignore`.
