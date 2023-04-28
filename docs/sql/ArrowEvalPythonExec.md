---
title: ArrowEvalPythonExec
---

# ArrowEvalPythonExec Physical Operator

`ArrowEvalPythonExec` is an [EvalPythonExec](EvalPythonExec.md) physical operator with [PythonSQLMetrics](PythonSQLMetrics.md) that represents [ArrowEvalPython](ArrowEvalPython.md) logical operator at execution time.

## Creating Instance

`ArrowEvalPythonExec` takes the following to be created:

* <span id="udfs"> [Scalar PythonUDF](PythonUDF.md#isScalarPythonUDF)s
* <span id="resultAttrs"> Result `Attribute`s ([Spark SQL]({{ book.spark_sql }}/expressions/Attribute))
* <span id="child"> Child `SparkPlan` ([Spark SQL]({{ book.spark_sql }}/physical-operators/SparkPlan))
* <span id="evalType"> Eval Type

`ArrowEvalPythonExec` is created when:

* `PythonEvals` physical execution strategy is executed (and plans [ArrowEvalPython](ArrowEvalPython.md) logical operators)
