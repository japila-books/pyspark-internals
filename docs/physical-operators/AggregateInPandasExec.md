# AggregateInPandasExec Physical Operator

`AggregateInPandasExec` is a unary physical operator ([Spark SQL]({{ book.spark_sql }}/physical-operators/UnaryExecNode)).

## Creating Instance

`AggregateInPandasExec` takes the following to be created:

* <span id="groupingExpressions"> Grouping Expressions ([Spark SQL]({{ book.spark_sql }}/expressions/Expression)) (`Seq[NamedExpression]`)
* <span id="udfExpressions"> [PythonUDF](../PythonUDF.md)s
* <span id="resultExpressions"> Result Named Expressions ([Spark SQL]({{ book.spark_sql }}/expressions/NamedExpression)) (`Seq[NamedExpression]`)
* <span id="child"> Child Physical Operator ([Spark SQL]({{ book.spark_sql }}/physical-operators/SparkPlan))

`AggregateInPandasExec` is created when `Aggregation` execution planning strategy ([Spark SQL]({{ book.spark_sql }}/execution-planning-strategies/Aggregation)) is executed for `Aggregate` logical operators ([Spark SQL]({{ book.spark_sql }}/logical-operators/Aggregate)) with [PythonUDF](../PythonUDF.md) aggregate expressions only.

## <span id="doExecute"> Executing Operator

```scala
doExecute(): RDD[InternalRow]
```

`doExecute` uses [ArrowPythonRunner](../ArrowPythonRunner.md) (one per partition) to execute [PythonUDFs](#udfExpressions).

`doExecute` is part of the `SparkPlan` ([Spark SQL]({{ book.spark_sql }}/physical-operators/SparkPlan#doExecute)) abstraction.
