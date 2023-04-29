---
title: ArrowEvalPython
---

# ArrowEvalPython Logical Operator

`ArrowEvalPython` is a [BaseEvalPython](BaseEvalPython.md) unary logical operator that evaluates [scalar PythonUDF](PythonUDF.md#isScalarPythonUDF)s with [Apache Arrow]({{ arrow.home }}).

`ArrowEvalPython` is planned as [ArrowEvalPythonExec](ArrowEvalPythonExec.md) physical operator.

## Creating Instance

`ArrowEvalPython` takes the following to be created:

* <span id="udfs"> [Scalar PythonUDF](PythonUDF.md#isScalarPythonUDF)s
* <span id="resultAttrs"> Result `Attribute`s ([Spark SQL]({{ book.spark_sql }}/expressions/Attribute))
* <span id="child"> Child `LogicalPlan` ([Spark SQL]({{ book.spark_sql }}/logical-operators/LogicalPlan))
* [Eval Type](#evalType)

`ArrowEvalPython` is created when:

* `ExtractPythonUDFs` logical optimization is executed (and requested to extract [scalar PythonUDF](PythonUDF.md#isScalarPythonUDF)s from a logical query plan)

### evalType { #evalType }

```scala
evalType: Int
```

`ArrowEvalPython` is given an `evalType` when [created](#creating-instance) that can only be one of the following:

* [SQL_SCALAR_PANDAS_UDF](../sql/PythonEvalType.md#SQL_SCALAR_PANDAS_UDF)
* [SQL_SCALAR_PANDAS_ITER_UDF](../sql/PythonEvalType.md#SQL_SCALAR_PANDAS_ITER_UDF)
