---
title: FlatMapGroupsInPandasExec
---

# FlatMapGroupsInPandasExec Physical Operator

`FlatMapGroupsInPandasExec` is a unary physical operator ([Spark SQL]({{ book.spark_sql }}/physical-operators/UnaryExecNode)) to execute a [PythonUDF](#func) using [ArrowPythonRunner](../runners/ArrowPythonRunner.md) (in [SQL_GROUPED_MAP_PANDAS_UDF](PythonEvalType.md#SQL_GROUPED_MAP_PANDAS_UDF) eval mode).

`FlatMapGroupsInPandasExec` represents a [FlatMapGroupsInPandas](FlatMapGroupsInPandas.md) logical operator at execution time.

## Creating Instance

`FlatMapGroupsInPandasExec` takes the following to be created:

* <span id="groupingAttributes"> Grouping Attributes ([Spark SQL]({{ book.spark_sql }}/expressions/Attribute))
* <span id="func"> Function Expression ([Spark SQL]({{ book.spark_sql }}/expressions/Expression))
* <span id="output"> Output Attributes ([Spark SQL]({{ book.spark_sql }}/expressions/Attribute))
* <span id="child"> Child Physical Operator ([Spark SQL]({{ book.spark_sql }}/physical-operators/SparkPlan))

`FlatMapGroupsInPandasExec` is created when:

* `BasicOperators` ([Spark SQL]({{ book.spark_sql }}/execution-planning-strategies/BasicOperators/)) execution planning strategy is executed (on a logical query plan with [FlatMapGroupsInPandas](FlatMapGroupsInPandas.md) logical operators)

## Performance Metrics

`ArrowEvalPythonExec` is a [PythonSQLMetrics](PythonSQLMetrics.md).

## Executing Operator { #doExecute }

??? note "SparkPlan"

    ```scala
    doExecute(): RDD[InternalRow]
    ```

    `doExecute` is part of the `SparkPlan` ([Spark SQL]({{ book.spark_sql }}/physical-operators/SparkPlan#doExecute)) abstraction.

`doExecute` requests the [child physical operator](#child) to `execute` (and produce a `RDD[InternalRow]`).

For every non-empty partition (using `RDD.mapPartitionsInternal`), `doExecute` creates an [ArrowPythonRunner](../runners/ArrowPythonRunner.md) (with [SQL_GROUPED_MAP_PANDAS_UDF](PythonEvalType.md#SQL_GROUPED_MAP_PANDAS_UDF) eval type) and [executePython](PandasGroupUtils.md#executePython).
