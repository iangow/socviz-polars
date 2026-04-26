# Data

The Parquet files in this directory are book inputs.

The maintainer-facing code that regenerates these files lives in the `data-raw/` directory of the `socviz_py` package. 
That package also bundles the same Parquet files for use via `socviz_pl.load_data()`:

```python
from socviz_pl import load_data

gss_sm = load_data("gss_sm")
```
