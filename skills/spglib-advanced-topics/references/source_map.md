# spglib source map: Advanced Topics

Generated from source roots:
- `cmake`
- `database`
- `fortran`
- `include`
- `python`
- `ruby`
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `SpglibDataset`
- `SpglibMagneticDataset`
- `msg`
- `database`
- `benchmark`
- `codespell`

## Fast source navigation
- `rg -n "SpglibDataset|SpglibMagneticDataset|msg|magnetic|benchmark" include src database test`
- `rg -n "codespell" pyproject.toml docs/codespell.txt`

## Function-level behavior checks
- Dataset and magnetic dataset contracts:
  `rg -n "SpglibDataset|SpglibMagneticDataset|spg_get_dataset|spg_get_magnetic_dataset" include/spglib.h`
- Magnetic database call chain:
  `rg -n "msg_identify_magnetic_space_group_type|msgdb_get_magnetic_spacegroup_type" src/magnetic_spacegroup.c src/msg_database.c`
- Magnetic Hall/db generation scripts:
  `rg -n "MagneticHallSymbol|encode_magnetic_operation|magnetic_spacegroup_types" database/msg/*.py`
- Validation checkpoint: struct field names in docs align with header declarations and referenced generator scripts feed tables in `src/msg_database.c`.

## Suggested source entry points
- `include/spglib.h` | dataset and magnetic dataset struct contracts
- `src/spg_database.c` | non-magnetic database lookups
- `src/magnetic_spacegroup.c` | magnetic dataset pipeline
- `src/msg_database.c` | magnetic space-group DB integration
- `database/msg/magnetic_hall.py` | magnetic Hall data preparation
- `database/msg/make_msgtype_db.py` | magnetic type table generation
- `test/CMakeLists.txt` | benchmark/test orchestration context
- `pyproject.toml` | codespell ignore-word wiring
