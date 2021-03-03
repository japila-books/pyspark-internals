# FlatMapGroupsInPandasExec

`FlatMapGroupsInPandasExec` is a unary physical operator ([Spark SQL]({{ book.spark_sql }}/physical-operators/UnaryExecNode)) to execute a [PythonUDF](#func).

`FlatMapGroupsInPandasExec` represents a [FlatMapGroupsInPandas](FlatMapGroupsInPandas.md) logical operator at execution time.

## Creating Instance

`FlatMapGroupsInPandasExec` takes the following to be created:

* <span id="groupingAttributes"> Grouping Attributes ([Spark SQL]({{ book.spark_sql }}/expressions/Attribute))
* <span id="func"> Function Expression ([Spark SQL]({{ book.spark_sql }}/expressions/Expression))
* <span id="output"> Output Attributes ([Spark SQL]({{ book.spark_sql }}/expressions/Attribute))
* <span id="child"> Child Physical Operator ([Spark SQL]({{ book.spark_sql }}/physical-operators/SparkPlan))

`FlatMapGroupsInPandasExec` is created when:

* `BasicOperators` ([Spark SQL]({{ book.spark_sql }}/execution-planning-strategies/BasicOperators/)) execution planning strategy is executed (on a logical query plan with [FlatMapGroupsInPandas](FlatMapGroupsInPandas.md) logical operators)
