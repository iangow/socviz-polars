# Agent Notes

- Render the Quarto book with `uv run quarto render`, not plain `quarto render`.
  Running through uv keeps Quarto's Jupyter execution inside the project
  environment; plain Quarto may select an unrelated user Jupyter kernel and miss
  project dependencies.
