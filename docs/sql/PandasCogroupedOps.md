# PandasCogroupedOps

`PandasCogroupedOps` is a logical grouping created by [GroupedData.cogroup](GroupedData.md#cogroup) over two [GroupedData](GroupedData.md)s.

```py
from pyspark.sql.pandas.group_ops import PandasCogroupedOps
```

`PandasCogroupedOps` is included in `__all__` of `pyspark.sql` module (via `__init__.py`).

## Creating Instance

`PandasCogroupedOps` takes the following to be created:

* <span id="gd1"> [GroupedData](GroupedData.md)
* <span id="gd2"> [GroupedData](GroupedData.md)

`PandasCogroupedOps` is created when:

* `PandasGroupedOpsMixin` is requested to [cogroup](PandasGroupedOpsMixin.md#cogroup)

## applyInPandas { #applyInPandas }

```py
applyInPandas(
  self,
  func: "PandasCogroupedMapFunction", # (1)!
  schema: Union[StructType, str]
) -> DataFrame
```

1. 
```py
from pandas.core.frame import DataFrame as PandasDataFrame
DataFrameLike = PandasDataFrame
PandasCogroupedMapFunction = Union[
  # func: (pandas.DataFrame, pandas.DataFrame) -> pandas.DataFrame
  Callable[[DataFrameLike, DataFrameLike], DataFrameLike],
  # func: (groupKey(s), pandas.DataFrame, pandas.DataFrame) -> pandas.DataFrame
  Callable[[Any, DataFrameLike, DataFrameLike], DataFrameLike],
]
```

`applyInPandas` creates a [DataFrame](DataFrame.md) with the result of [flatMapCoGroupsInPandas](RelationalGroupedDataset.md#flatMapCoGroupsInPandas) with a [pandas user defined function](../pyspark/sql/pandas/functions.md#pandas_udf) of `SQL_COGROUPED_MAP_PANDAS_UDF` type.

---

`applyInPandas` [creates a pandas user defined function](../pyspark/sql/pandas/functions.md#pandas_udf) for the given `func` and the return type by the given `schema`. The pandas UDF is of `SQL_COGROUPED_MAP_PANDAS_UDF` type.

`applyInPandas` applies the pandas UDF on all the columns of the two [GroupedData](#creating-instance)s (that creates a `Column` expression).

`applyInPandas` requests the [GroupedData](#gd1) for the associated [RelationalGroupedDataset](GroupedData.md#jgd) that is in turn requested to [flatMapCoGroupsInPandas](RelationalGroupedDataset.md#flatMapCoGroupsInPandas).

### Example { #applyInPandas-example }

```py
df1 = spark.createDataFrame(
    data = [
      (20000101, 1, 1.0),
      (20000101, 2, 2.0),
      (20000102, 1, 3.0),
      (20000102, 2, 4.0)],
    schema = ("time", "id", "v1"))
df2 = spark.createDataFrame(
    data = [
      (20000101, 1, "x"),
      (20000101, 2, "y")],
    schema = ("time", "id", "v2"))
```

```py
import pandas as pd
def asof_join(k, l, r):
  if k == (1,):
    return pd.merge_asof(l, r, on="time", by="id")
  else:
    return pd.DataFrame(columns=['time', 'id', 'v1', 'v2'])
```

```py
gd1 = df1.groupby("id")
gd2 = df2.groupby("id")
```

```py
gd1
  .cogroup(gd2)
  .applyInPandas(
    asof_join,
    "time int, id int, v1 double, v2 string")
  .show()
```
