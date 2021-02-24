# PandasGroupedOpsMixin

## <span id="applyInPandas"> applyInPandas

```scala
applyInPandas(
  self,
  func,
  schema)
```

`applyInPandas` creates a `DataFrame` with [flatMapGroupsInPandas](RelationalGroupedDataset.md#flatMapGroupsInPandas).

### <span id="applyInPandas-example"> Example

```text
def asof_join(k, l, r):
  if k == (1,):
    return pd.merge_asof(l, r, on="time", by="id")
  else:
    return pd.DataFrame(columns=['time', 'id', 'v1', 'v2'])
df1.groupby("id").cogroup(df2.groupby("id")).applyInPandas(
  asof_join, "time int, id int, v1 double, v2 string").show()
```
