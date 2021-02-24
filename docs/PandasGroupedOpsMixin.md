# PandasGroupedOpsMixin

`PandasGroupedOpsMixin` is a Python mixin for [GroupedData](GroupedData.md) class.

## <span id="applyInPandas"> applyInPandas

```scala
applyInPandas(
  self,
  func,
  schema)
```

`applyInPandas` creates a `DataFrame` with [flatMapGroupsInPandas](RelationalGroupedDataset.md#flatMapGroupsInPandas).

### <span id="applyInPandas-example"> Example

```python
df1 = spark.createDataFrame(
    [(20000101, 1, 1.0), (20000101, 2, 2.0), (20000102, 1, 3.0), (20000102, 2, 4.0)],
    ("time", "id", "v1"))
df2 = spark.createDataFrame(
    [(20000101, 1, "x"), (20000101, 2, "y")],
    ("time", "id", "v2"))
import pandas as pd
def asof_join(k, l, r):
  if k == (1,):
    return pd.merge_asof(l, r, on="time", by="id")
  else:
    return pd.DataFrame(columns=['time', 'id', 'v1', 'v2'])
df1.groupby("id").cogroup(df2.groupby("id")).applyInPandas(
  asof_join, "time int, id int, v1 double, v2 string").show()
```
