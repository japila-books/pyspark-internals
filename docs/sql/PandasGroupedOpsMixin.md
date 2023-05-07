# PandasGroupedOpsMixin

`PandasGroupedOpsMixin` is a Python mixin for [GroupedData](GroupedData.md) class.

## applyInPandas { #applyInPandas }

```py
applyInPandas(
  self,
  func: "PandasGroupedMapFunction", # (1)!
  schema: Union[StructType, str]
) -> DataFrame
```

1. 
```py
from pandas.core.frame import DataFrame as PandasDataFrame
DataFrameLike = PandasDataFrame
PandasGroupedMapFunction = Union[
  # func: pandas.DataFrame -> pandas.DataFrame
  Callable[[DataFrameLike], DataFrameLike],
  # func: (groupKey(s), pandas.DataFrame) -> pandas.DataFrame
  Callable[[Any, DataFrameLike], DataFrameLike],
]
```

`applyInPandas` creates a [pandas_udf](../pyspark/sql/pandas/functions.md#pandas_udf) with the following:

pandas_udf | Value
-----------|------
 `f` | The given `func`
 `returnType` | The given `schema`
 `functionType` | [PandasUDFType.GROUPED_MAP](../pyspark/sql/pandas/PandasUDFType.md#GROUPED_MAP)

`applyInPandas` creates a `Column` wtih the `pandas_udf` applied to all the columns of the [DataFrame](GroupedData.md#_df) of this [GroupedData](GroupedData.md).

`applyInPandas` requests the [RelationalGroupedDataset](#_jgd) to [flatMapGroupsInPandas](RelationalGroupedDataset.md#flatMapGroupsInPandas) with the underlying Catalyst expression of the `Column` with the `pandas_udf`.

In the end, `applyInPandas` creates a [DataFrame](DataFrame.md) with the result.

## cogroup { #cogroup }

```py
cogroup(
  self,
  other: "GroupedData") -> "PandasCogroupedOps"
```

`cogroup` creates a [PandasCogroupedOps](PandasCogroupedOps.md) for this and the other [GroupedData](GroupedData.md)s.
