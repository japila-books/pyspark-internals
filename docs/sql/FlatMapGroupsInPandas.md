# FlatMapGroupsInPandas

`FlatMapGroupsInPandas` is a unary logical operator ([Spark SQL]({{ book.spark_sql }}/logical-operators/LogicalPlan/#UnaryNode)).

`FlatMapGroupsInPandas` is planned as a [FlatMapGroupsInPandasExec](FlatMapGroupsInPandasExec.md) physical operator.

## Creating Instance

`FlatMapGroupsInPandas` takes the following to be created:

* <span id="groupingAttributes"> Grouping Attributes ([Spark SQL]({{ book.spark_sql }}/expressions/Attribute))
* <span id="functionExpr"> Function Expression ([Spark SQL]({{ book.spark_sql }}/expressions/Expression))
* <span id="output"> Output Attributes ([Spark SQL]({{ book.spark_sql }}/expressions/Attribute))
* <span id="child"> Child Logical Operator ([Spark SQL]({{ book.spark_sql }}/logical-operators/LogicalPlan))

`FlatMapGroupsInPandas` is created when:

* `RelationalGroupedDataset` is requested to [flatMapGroupsInPandas](RelationalGroupedDataset.md#flatMapGroupsInPandas) (with a [PythonUDF](PythonUDF.md))
