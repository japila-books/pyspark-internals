---
title: AggregateInPandasExec
---

# AggregateInPandasExec Physical Operator

`AggregateInPandasExec` is a unary physical operator ([Spark SQL]({{ book.spark_sql }}/physical-operators/UnaryExecNode)) that executes [pandas UDAFs](#udfExpressions) using [ArrowPythonRunner](../runners/ArrowPythonRunner.md) (one per partition).

## Creating Instance

`AggregateInPandasExec` takes the following to be created:

* <span id="groupingExpressions"> Grouping Expressions ([Spark SQL]({{ book.spark_sql }}/expressions/Expression)) (`Seq[NamedExpression]`)
* <span id="udfExpressions"> pandas UDAFs ([PythonUDF](PythonUDF.md)s with [SQL_GROUPED_AGG_PANDAS_UDF](PythonEvalType.md#SQL_GROUPED_AGG_PANDAS_UDF))
* <span id="resultExpressions"> Result Named Expressions ([Spark SQL]({{ book.spark_sql }}/expressions/NamedExpression)) (`Seq[NamedExpression]`)
* <span id="child"> Child Physical Operator ([Spark SQL]({{ book.spark_sql }}/physical-operators/SparkPlan))

`AggregateInPandasExec` is created when `Aggregation` execution planning strategy ([Spark SQL]({{ book.spark_sql }}/execution-planning-strategies/Aggregation)) is executed for `Aggregate` logical operators ([Spark SQL]({{ book.spark_sql }}/logical-operators/Aggregate)) with [PythonUDF](PythonUDF.md) aggregate expressions only.

## Executing Operator { #doExecute }

??? note "SparkPlan"

    ```scala
    doExecute(): RDD[InternalRow]
    ```

    `doExecute` is part of the `SparkPlan` ([Spark SQL]({{ book.spark_sql }}/physical-operators/SparkPlan#doExecute)) abstraction.

`doExecute` uses [ArrowPythonRunner](../runners/ArrowPythonRunner.md) (one per partition) to execute [PythonUDFs](#udfExpressions).
