# RelationalGroupedDataset

`RelationalGroupedDataset` is a result of executing high-level grouping operators.

!!! note "This is a stub"
    This page is a stub to describe PySpark-related methods only. Learn more about [RelationalGroupedDataset]({{ book.spark_sql }}/RelationalGroupedDataset/) in [The Internals of Spark SQL]({{ book.spark_sql }}).

## flatMapCoGroupsInPandas { #flatMapCoGroupsInPandas }

```scala
flatMapCoGroupsInPandas(
  r: RelationalGroupedDataset,
  expr: PythonUDF): DataFrame
```

`flatMapCoGroupsInPandas`...FIXME

---

`flatMapCoGroupsInPandas` is used when:

* `PandasCogroupedOps` is requested to [applyInPandas](PandasCogroupedOps.md#applyInPandas)

## flatMapGroupsInPandas { #flatMapGroupsInPandas }

```scala
flatMapGroupsInPandas(
  expr: PythonUDF): DataFrame
```

`flatMapGroupsInPandas` creates a `DataFrame` with a [FlatMapGroupsInPandas](FlatMapGroupsInPandas.md) logical operator (to execute the given [PythonUDF](PythonUDF.md)).

---

`flatMapGroupsInPandas` asserts that the input [PythonUDF](PythonUDF.md) is a grouped map udf (the [eval type](PythonUDF.md#evalType) is [SQL_GROUPED_MAP_PANDAS_UDF](PythonEvalType.md#SQL_GROUPED_MAP_PANDAS_UDF)).

`flatMapGroupsInPandas` asserts that the [return type](PythonUDF.md#dataType) of the input [PythonUDF](PythonUDF.md) is `StructType`.

---

`flatMapGroupsInPandas` is used when:

* `PandasGroupedOpsMixin` is requested to [applyInPandas](PandasGroupedOpsMixin.md#applyInPandas)
