# PythonArrowOutput

`PythonArrowOutput` is an [extension](#contract) of the [BasePythonRunner](BasePythonRunner.md) abstraction for [vectorized (ColumnarBatch) runners](#implementations).

??? note "Scala Definition"

    ```scala
    trait PythonArrowOutput[OUT <: AnyRef] {
        self: BasePythonRunner[_, OUT] =>
        // ...
    }
    ```

## Contract

### Deserializing ColumnarBatch { #deserializeColumnarBatch }

```scala
deserializeColumnarBatch(
  batch: ColumnarBatch,
  schema: StructType): OUT
```

See:

* [BasicPythonArrowOutput](BasicPythonArrowOutput.md#deserializeColumnarBatch)

Used when:

* `PythonArrowOutput` is requested to [newReaderIterator](#newReaderIterator) (after a batch is loaded)

### Performance Metrics { #pythonMetrics }

```scala
pythonMetrics: Map[String, SQLMetric]
```

`SQLMetric`s ([Spark SQL]({{ book.spark_sql }}/SQLMetric)):

* `pythonNumRowsReceived`
* `pythonDataReceived`

Used when:

* `PythonArrowOutput` is requested to [newReaderIterator](#newReaderIterator) (after a batch is loaded)

## Implementations

* `ApplyInPandasWithStatePythonRunner`
* [BasicPythonArrowOutput](BasicPythonArrowOutput.md)
