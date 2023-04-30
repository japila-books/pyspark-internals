# GroupedData

`GroupedData` is created for the following `DataFrame` operators:

* [cube](DataFrame.md#cube)
* [groupBy](DataFrame.md#groupBy)
* [rollup](DataFrame.md#rollup)
* [pivot](DataFrame.md#pivot)

[GroupedData.agg](#agg) is used to apply aggregation functions to groups of rows (_execution environment_):

* Built-In Aggregation Functions
* [Group Aggregate pandas UDFs](../pandas-udfs/index.md#group-aggregate)

`GroupedData` is a Python class with [PandasGroupedOpsMixin](PandasGroupedOpsMixin.md) mixin.

`GroupedData` is defined in `pyspark.sql.group` module.

```py
from pyspark.sql.group import GroupedData
```

## Creating Instance

`GroupedData` takes the following to be created:

* <span id="jgd"> [RelationalGroupedDataset](RelationalGroupedDataset.md)
* <span id="df"> [DataFrame](DataFrame.md)

## agg

```py
agg(
    self,
    *exprs: Union[Column, Dict[str, str]]) -> DataFrame
```

!!! note
    Built-in aggregation functions and [group aggregate pandas UDFs](../pandas-udfs/index.md#group-aggregate) cannot be mixed in a single `agg`.
