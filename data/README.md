# Data

The Parquet files are exported from data objects in the `socviz` repository.

Regenerate them with:

```sh
curl -L -o /tmp/gss_sm.rda https://github.com/kjhealy/socviz/raw/refs/heads/main/data/gss_sm.rda
curl -L -o /tmp/organdata.rda https://github.com/kjhealy/socviz/raw/refs/heads/main/data/organdata.rda
curl -L -o /tmp/elections_historic.rda https://github.com/kjhealy/socviz/raw/refs/heads/main/data/elections_historic.rda
curl -L -o /tmp/election.rda https://github.com/kjhealy/socviz/raw/refs/heads/main/data/election.rda
curl -L -o /tmp/county_map.rda https://github.com/kjhealy/socviz/raw/refs/heads/main/data/county_map.rda
curl -L -o /tmp/county_data.rda https://github.com/kjhealy/socviz/raw/refs/heads/main/data/county_data.rda
curl -L -o /tmp/opiates.rda https://github.com/kjhealy/socviz/raw/refs/heads/main/data/opiates.rda
curl -L -o /tmp/titanic.rda https://github.com/kjhealy/socviz/raw/refs/heads/main/data/titanic.rda
curl -L -o /tmp/oecd_sum.rda https://github.com/kjhealy/socviz/raw/refs/heads/main/data/oecd_sum.rda
Rscript -e '
  write_clean_parquet <- function(rda_path, object_name, parquet_path) {
    load(rda_path)
    x <- get(object_name)
    x <- as.data.frame(lapply(x, function(col) {
      if (inherits(col, "Date")) col
      else if (is.factor(col)) as.character(col)
      else if (is.numeric(col)) as.numeric(col)
      else as.vector(col)
    }), stringsAsFactors = FALSE)
    arrow::write_parquet(x, parquet_path)
  }

  write_clean_parquet("/tmp/gss_sm.rda", "gss_sm", "data/gss_sm.parquet")
  write_clean_parquet("/tmp/organdata.rda", "organdata", "data/organdata.parquet")
  write_clean_parquet(
    "/tmp/elections_historic.rda",
    "elections_historic",
    "data/elections_historic.parquet"
  )
  write_clean_parquet("/tmp/election.rda", "election", "data/election.parquet")
  write_clean_parquet("/tmp/county_map.rda", "county_map", "data/county_map.parquet")
  write_clean_parquet("/tmp/county_data.rda", "county_data", "data/county_data.parquet")
  write_clean_parquet("/tmp/opiates.rda", "opiates", "data/opiates.parquet")
  write_clean_parquet("/tmp/titanic.rda", "titanic", "data/titanic.parquet")
  write_clean_parquet("/tmp/oecd_sum.rda", "oecd_sum", "data/oecd_sum.parquet")
'
```

In Python:

```python
import polars as pl

gss_sm = pl.read_parquet("data/gss_sm.parquet")
```
