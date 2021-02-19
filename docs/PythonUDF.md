# PythonUDF

`PythonUDF` is a Catalyst expression ([Spark SQL]({{ book.spark_sql }}/expressions/Expression)).

## Creating Instance

`PythonUDF` takes the following to be created:

* <span id="name"> Name
* <span id="func"> [PythonFunction](PythonFunction.md)
* <span id="dataType"> `DataType` ([Spark SQL]({{ book.spark_sql }}/DataType))
* <span id="children"> Children Catalyst Expressions ([Spark SQL]({{ book.spark_sql }}/expressions/Expression))
* <span id="evalType"> Python Eval Type
* <span id="udfDeterministic"> `udfDeterministic` flag
* <span id="resultId"> Result ID (`ExprId`)

`PythonUDF` is created when:

* `UserDefinedPythonFunction` is requested to [builder](UserDefinedPythonFunction.md#builder)

## Unevaluable

`PythonUDF` is an `Unevaluable` expression ([Spark SQL]({{ book.spark_sql }}/expressions/Unevaluable)).

## NonSQLExpression

`PythonUDF` is a `NonSQLExpression` expression ([Spark SQL]({{ book.spark_sql }}/expressions/NonSQLExpression)).

## UserDefinedExpression

`PythonUDF` is a `UserDefinedExpression` expression ([Spark SQL]({{ book.spark_sql }}/expressions/UserDefinedExpression)).
