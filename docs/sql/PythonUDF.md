# PythonUDF

`PythonUDF` is a Catalyst expression ([Spark SQL]({{ book.spark_sql }}/expressions/Expression)).

## Creating Instance

`PythonUDF` takes the following to be created:

* <span id="name"> Name
* <span id="func"> [PythonFunction](../PythonFunction.md)
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

## isScalarPythonUDF { #isScalarPythonUDF }

```scala
isScalarPythonUDF(
  e: Expression): Boolean
```

`isScalarPythonUDF` holds `true` when the following all hold `true`:

* The given `Expression` ([Spark SQL]({{ book.spark_sql }}/expressions/Expression)) is a [PythonUDF](PythonUDF.md)
* The [evalType](#evalType) is [scalar](#SCALAR_TYPES)

---

`isScalarPythonUDF` is used when:

* `ExtractPythonUDFFromJoinCondition` is requested to `hasUnevaluablePythonUDF`
* `ExtractPythonUDFFromAggregate` is requested to `hasPythonUdfOverAggregate`
* `ExtractGroupingPythonUDFFromAggregate` is requested to `hasScalarPythonUDF`
* `ExtractPythonUDFs` is requested to `hasScalarPythonUDF`, `collectEvaluableUDFs`, `extract`

## Scalar PythonUDF Types { #SCALAR_TYPES }

`PythonUDF` is [scalar](#isScalarPythonUDF) for the following eval types:

* `SQL_BATCHED_UDF` (`100`)
* `SQL_SCALAR_PANDAS_UDF` (`200`)
* `SQL_SCALAR_PANDAS_ITER_UDF` (`204`)
