# Agent Notes

- Render the Quarto book with `uv run quarto render`, not plain `quarto render`.
  Running through uv keeps Quarto's Jupyter execution inside the project
  environment; plain Quarto may select an unrelated user Jupyter kernel and miss
  project dependencies.
- `socviz_py` is the distribution package, but this Polars-oriented book should
  import user-facing helpers through `socviz_pl`. Keep plot themes and data
  helpers exposed there so a future pandas-oriented API can live alongside it.
