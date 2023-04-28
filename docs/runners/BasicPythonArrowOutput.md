# BasicPythonArrowOutput

`BasicPythonArrowOutput` is a marker extension of the [PythonArrowOutput](PythonArrowOutput.md) abstraction for [vectorized outputs](#implementations) of [BasePythonRunner](BasePythonRunner.md)s that produce `ColumnarBatch`es ([Spark SQL]({{ book.spark_sql }}/vectorized-query-execution/ColumnarBatch)).

## Implementations

* [ArrowPythonRunner](ArrowPythonRunner.md)
* `CoGroupedArrowPythonRunner`

## Deserializing ColumnarBatch { #deserializeColumnarBatch }

??? note "PythonArrowOutput"

    ```scala
    deserializeColumnarBatch(
      batch: ColumnarBatch,
      schema: StructType): ColumnarBatch
    ```

    `deserializeColumnarBatch` is part of the [PythonArrowOutput](PythonArrowOutput.md#deserializeColumnarBatch) abstraction.

`deserializeColumnarBatch` returns the given `ColumnarBatch` unchanged.
