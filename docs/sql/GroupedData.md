# GroupedData

`GroupedData` is created for the following high-level operators:

* [DataFrame.cube](DataFrame.md#cube)
* [DataFrame.groupBy](DataFrame.md#groupBy)
* [DataFrame.rollup](DataFrame.md#rollup)
* [GroupedData.pivot](#pivot)

`GroupedData` is then used to execute aggregate functions (over groups of rows) using [agg](#agg) operator:

* Built-In Aggregation Functions
* [pandas UDAFs](../pandas-udafs/index.md)

`GroupedData` is a Python class with [PandasGroupedOpsMixin](PandasGroupedOpsMixin.md) mixin.

`GroupedData` is defined in [pyspark.sql.group](../pyspark/sql/group.md) module.

```py
from pyspark.sql.group import GroupedData
```

## Creating Instance

`GroupedData` takes the following to be created:

* <span id="jgd"><span id="_jgd"> [RelationalGroupedDataset](RelationalGroupedDataset.md)
* <span id="df"><span id="_df"> [DataFrame](DataFrame.md)

## agg

```py
agg(
  self,
  *exprs: Union[Column, Dict[str, str]]) -> DataFrame
```

!!! note
    Built-in aggregation functions and [pandas UDAFs](../pandas-udafs/index.md) cannot be used together in a single `agg`.

`agg` accepts a collection of `Column` expressions or a single `Dict[str, str]` object.

`agg` requests the [RelationalGroupedDataset](#_jgd) to `agg` ([Spark SQL]({{ book.spark_sql }}/RelationalGroupedDataset/#agg)).

In the end, `agg` creates a [DataFrame](DataFrame.md) with the `agg` result.
