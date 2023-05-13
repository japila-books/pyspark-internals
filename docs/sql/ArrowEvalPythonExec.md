---
title: ArrowEvalPythonExec
---

# ArrowEvalPythonExec Physical Operator

`ArrowEvalPythonExec` is an [EvalPythonExec](EvalPythonExec.md) physical operator to [evaluate scalar PythonUDFs](#evaluate) using [ArrowPythonRunner](../runners/ArrowPythonRunner.md).

`ArrowEvalPythonExec` represents [ArrowEvalPython](ArrowEvalPython.md) logical operator at execution time.

## Creating Instance

`ArrowEvalPythonExec` takes the following to be created:

* <span id="udfs"> [Scalar PythonUDF](PythonUDF.md#isScalarPythonUDF)s
* <span id="resultAttrs"> Result `Attribute`s ([Spark SQL]({{ book.spark_sql }}/expressions/Attribute))
* <span id="child"> Child `SparkPlan` ([Spark SQL]({{ book.spark_sql }}/physical-operators/SparkPlan))
* <span id="evalType"> Eval Type

`ArrowEvalPythonExec` is created when:

* `PythonEvals` physical execution strategy is executed (and plans [ArrowEvalPython](ArrowEvalPython.md) logical operators)

## Performance Metrics

`ArrowEvalPythonExec` is a [PythonSQLMetrics](PythonSQLMetrics.md).

## Maximum Records per Batch { #batchSize }

`batchSize` is the value of [spark.sql.execution.arrow.maxRecordsPerBatch](../configuration-properties/index.md#spark.sql.execution.arrow.maxRecordsPerBatch) configuration property.

`batchSize` is used while [evaluating PythonUDFs](#evaluate).

## Evaluating PythonUDFs { #evaluate }

??? note "EvalPythonExec"

    ```scala
    evaluate(
      funcs: Seq[ChainedPythonFunctions],
      argOffsets: Array[Array[Int]],
      iter: Iterator[InternalRow],
      schema: StructType,
      context: TaskContext): Iterator[InternalRow]
    ```

    `evaluate` is part of the [EvalPythonExec](EvalPythonExec.md#evaluate) abstraction.

`evaluate` creates an [ArrowPythonRunner](../runners/ArrowPythonRunner.md) to [compute partitions](../runners/BasePythonRunner.md#compute).

In the end, `evaluate` converts `ColumnarBatch`es into `InternalRow`s.
