---
name: spglib-advanced-topics
description: Consolidated advanced/low-frequency spglib topics merged from one-doc skills to reduce routing noise while preserving references.
---

# spglib: Advanced Topics

## High-Signal Playbook

### Route conditions
- Use `spglib-api-and-scripting` for API-call selection and lifecycle details.
- Use `spglib-developer-guide` for contributor workflows and broad test orchestration.
- Use `spglib-simulation-workflows` for end-to-end runnable example setup.

### Triage questions
- Is this about dataset field interpretation or magnetic dataset internals?
- Is the issue documentation semantics, runtime behavior, or generated database content?
- Is performance benchmarking required, or only correctness checks?

### Canonical workflow
1. Resolve terminology in docs first (`docs/dataset.md`, `docs/magnetic_dataset.md`, `docs/development/performance.md`).
2. Reproduce behavior with a minimal dataset call before source deep-dive.
3. Probe magnetic/database functions in `src/msg_database.c` and `src/magnetic_spacegroup.c` when docs are ambiguous.
4. Use benchmark command only after correctness baseline is stable.

### Minimal working example
```bash
python - <<'PY'
import spglib
cell = (
    [[3.111, 0, 0], [-1.5555, 2.6942050311733885, 0], [0, 0, 4.988]],
    [[1/3, 2/3, 0.0], [2/3, 1/3, 0.5], [1/3, 2/3, 0.6181], [2/3, 1/3, 0.1181]],
    [1, 1, 2, 2],
)
dset = spglib.get_symmetry_dataset(cell, symprec=1e-5)
print(dset.number, dset.international, len(dset.equivalent_atoms))
PY
pytest --benchmark-only --benchmark-columns=mean,stddev -s -v test/test_benchmark.py
```

### Convergence and validation checks
- Baseline dataset call returns non-empty `equivalent_atoms` and operation metadata.
- Field names and meanings match `docs/dataset.md` / `docs/magnetic_dataset.md`.
- Magnetic dataset behavior is stable across repeated runs with fixed inputs.
- Benchmark output completes without functional regressions.

## Scope
- Handle lower-frequency topics merged from one-doc skills:
  - dataset field reference details
  - magnetic dataset field reference details
  - codespell dictionary/ignore list
  - startup/testing architecture pointers
  - performance benchmark note

## Route the request
- Dataset/API usage questions with runnable context -> `spglib-api-and-scripting`.
- Input-convention and tolerance interpretation -> `spglib-inputs-and-modeling` or `spglib-variable`.
- Contributor test/performance workflows -> `spglib-developer-guide`.
- Example execution tasks -> `spglib-simulation-workflows`.

## Primary documentation references
- `docs/dataset.md`
- `docs/magnetic_dataset.md`
- `docs/codespell.txt`
- `test/README.md`
- `docs/development/performance.md`

## Workflow
- Start from primary references.
- Use `references/doc_map.md` for the merged inventory.
- Escalate to `references/source_map.md` only for unresolved implementation details.
- Cite exact file paths used.

## Source entry points for unresolved issues
- `include/spglib.h`
- `src/spg_database.c`
- `src/magnetic_spacegroup.c`
- `src/msg_database.c`
- `database/msg/magnetic_hall.py`
- `database/msg/make_msgtype_db.py`
- `test/CMakeLists.txt`
- `pyproject.toml`
