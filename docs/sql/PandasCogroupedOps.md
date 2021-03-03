# PandasCogroupedOps

`PandasCogroupedOps` is a logical grouping created by [GroupedData.cogroup](GroupedData.md#cogroup).

```python
from pyspark.sql.pandas.group_ops import PandasCogroupedOps
```

`PandasCogroupedOps` is included in `__all__` of `pyspark.sql` module (via `__init__.py`).

## Creating Instance

`PandasCogroupedOps` takes the following to be created:

* <span id="gd1"> [GroupedData](GroupedData.md)
* <span id="gd2"> [GroupedData](GroupedData.md)

`PandasCogroupedOps` is created when:

* `PandasGroupedOpsMixin` is requested to [cogroup](PandasGroupedOpsMixin.md#cogroup)

## <span id="applyInPandas"> applyInPandas

```python
applyInPandas(self, func, schema)
```

`applyInPandas` creates a [DataFrame](DataFrame.md) with the result of [flatMapCoGroupsInPandas](RelationalGroupedDataset.md#flatMapCoGroupsInPandas) with a [pandas user defined function](../pyspark/sql/pandas/functions.md#pandas_udf) of `SQL_COGROUPED_MAP_PANDAS_UDF` type.

---

`applyInPandas` [creates a pandas user defined function](../pyspark/sql/pandas/functions.md#pandas_udf) for the given `func` and the return type by the given `schema`. The pandas UDF is of `SQL_COGROUPED_MAP_PANDAS_UDF` type.

`applyInPandas` applies the pandas UDF on all the columns of the two [GroupedData](#creating-instance)s (that creates a `Column` expression).

`applyInPandas` requests the [GroupedData](#gd1) for the associated [RelationalGroupedDataset](GroupedData.md#jgd) that is in turn requested to [flatMapCoGroupsInPandas](RelationalGroupedDataset.md#flatMapCoGroupsInPandas).
