# Naming conventions

Use these prefixes consistently.

- `src__` - source-entry models that map closely to the raw files
- `stg__` - cleaned staging models
- `dim__` - dimensions
- `int__` - intermediate bridge and path models
- `mart__` - analysis-ready marts
- `diag__` - diagnostic findings
- `obs__` - final observatory outputs

## Additional rules

- Use lowercase snake_case after the prefix.
- Prefer stable business nouns over generic names like `final_table`.
- Do not create duplicate semantic models under different names.
- Do not use date-suffixed model names unless the model itself is snapshot-like by design.
