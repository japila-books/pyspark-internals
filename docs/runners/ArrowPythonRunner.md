# ArrowPythonRunner

`ArrowPythonRunner` is a [BasePythonRunner](BasePythonRunner.md) with `Iterator[InternalRow]` input and `ColumnarBatch` (vectorized) output.

`ArrowPythonRunner` supports `BasicPythonArrowInput` and [BasicPythonArrowOutput](BasicPythonArrowOutput.md).

## Creating Instance

`ArrowPythonRunner` takes the following to be created:

* <span id="funcs"> `ChainedPythonFunctions`es
* <span id="evalType"> Eval Type
* <span id="argOffsets"> Argument Offsets
* <span id="schema"> `Schema` ([Spark SQL]({{ book.spark_sql }}/types/StructType))
* <span id="timeZoneId"> TimeZone ID
* <span id="workerConf"> Worker Configuration
* <span id="pythonMetrics"> Performance Metrics

`ArrowPythonRunner` is created when the following physical operators ([Spark SQL]({{ book.spark_sql }}/physical-operators/)) are executed:

* [AggregateInPandasExec](../sql/AggregateInPandasExec.md)
* [ArrowEvalPythonExec](../sql/ArrowEvalPythonExec.md)
* `FlatMapGroupsInPandasExec`
* `MapInPandasExec`
* `WindowInPandasExec`

## bufferSize { #bufferSize }

??? note "BasePythonRunner"

    ```scala
    bufferSize: Int
    ```

    `bufferSize` is part of the [BasePythonRunner](BasePythonRunner.md#bufferSize) abstraction.

`bufferSize` is the value of [spark.sql.execution.pandas.udf.buffer.size](../configuration-properties.md#spark.sql.execution.pandas.udf.buffer.size) configuration property.

## simplifiedTraceback { #simplifiedTraceback }

??? note "BasePythonRunner"

    ```scala
    simplifiedTraceback: Boolean
    ```

    `simplifiedTraceback` is part of the [BasePythonRunner](BasePythonRunner.md#simplifiedTraceback) abstraction.

`simplifiedTraceback` is the value of [spark.sql.execution.pyspark.udf.simplifiedTraceback.enabled](../configuration-properties.md#spark.sql.execution.pyspark.udf.simplifiedTraceback.enabled) configuration property.
