# socviz-polars

## Rendering

Render the Quarto book through uv:

```sh
uv run quarto render
```

This keeps Quarto's Jupyter execution inside the project environment. Running
`quarto render` directly may select an unrelated Jupyter kernel, such as a
previously registered user kernel, and fail to find project dependencies.
