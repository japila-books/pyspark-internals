# BasePythonRunner

`BasePythonRunner` is an [abstraction](#contract) of [Python Runners](#implementations).

??? note "Scala Definition"

    `BasePythonRunner` is a type constructor in Scala (_generic class_ in Java) with the following definition:

    ```scala
    abstract class BasePythonRunner[IN, OUT](...) {
        // ...
    }
    ```

    `BasePythonRunner` uses `IN` and `OUT` as the name of the types for the input and output values.

## Contract

### <span id="newReaderIterator"> newReaderIterator

```scala
newReaderIterator(
  stream: DataInputStream,
  writerThread: WriterThread,
  startTime: Long,
  env: SparkEnv,
  worker: Socket,
  pid: Option[Int],
  releasedOrClosed: AtomicBoolean,
  context: TaskContext): Iterator[OUT]
```

See:

* [PythonRunner](PythonRunner.md#newReaderIterator)
* [PythonUDFRunner](PythonUDFRunner.md#newReaderIterator)

Used when:

* `BasePythonRunner` is requested to [compute](#compute)

### <span id="newWriterThread"> newWriterThread

```scala
newWriterThread(
  env: SparkEnv,
  worker: Socket,
  inputIterator: Iterator[IN],
  partitionIndex: Int,
  context: TaskContext): WriterThread
```

See:

* [PythonRunner](PythonRunner.md#newWriterThread)
* [PythonUDFRunner](PythonUDFRunner.md#newWriterThread)

Used when:

* `BasePythonRunner` is requested to [compute](#compute)

## Implementations

* `ApplyInPandasWithStatePythonRunner`
* [ArrowPythonRunner](ArrowPythonRunner.md)
* `CoGroupedArrowPythonRunner`
* [PythonRunner](PythonRunner.md)
* [PythonUDFRunner](PythonUDFRunner.md)

## Creating Instance

`BasePythonRunner` takes the following to be created:

* <span id="funcs"> `ChainedPythonFunctions`
* <span id="evalType"> Eval Type
* <span id="argOffsets"> Argument Offsets

`BasePythonRunner` requires that the number of [ChainedPythonFunctions](#funcs) and [Argument Offsets](#argOffsets) are the same.

!!! note "Abstract Class"
    `BasePythonRunner` is an abstract class and cannot be created directly. It is created indirectly for the [concrete BasePythonRunners](#implementations).

### <span id="maybeAccumulator"> accumulator { #accumulator }

```scala
accumulator: PythonAccumulatorV2
```

`BasePythonRunner` initializes a registry of a [PythonAccumulatorV2](../PythonAccumulatorV2.md) when [created](#creating-instance) to be the [accumulator](../PythonFunction.md#accumulator) of the head [PythonFunction](../PythonFunction.md) among the given [ChainedPythonFunctions](#funcs).

The `PythonAccumulatorV2` is used when `ReaderIterator` is requested to [handleEndOfDataSection](ReaderIterator.md#handleEndOfDataSection) (to update metrics).

## <span id="compute"> Computing Result

```scala
compute(
  inputIterator: Iterator[IN],
  partitionIndex: Int,
  context: TaskContext): Iterator[OUT]
```

`compute` makes sure that `spark.executorEnv.OMP_NUM_THREADS` configuration option is set or defaults to `spark.executor.cores` property.

`compute` defines the following environment variables:

* `SPARK_LOCAL_DIRS` to be the local directories of the local `DiskBlockManager`
* `SPARK_BUFFER_SIZE` to be the value of `spark.buffer.size` configuration property (default: `65536`)

`compute` can optionally define environment variables:

* `SPARK_REUSE_WORKER` to be `1` based on `spark.python.worker.reuse` configuration property (default: `true`)
* `PYSPARK_EXECUTOR_MEMORY_MB` to be the value of `spark.executor.pyspark.memory` configuration property if defined

`compute` requests the executor's `SparkEnv` to `createPythonWorker` (for a `pythonExec` and the environment variables) that requests [PythonWorkerFactory](../PythonWorkerFactory.md) to [create a Python worker](#create) (and give a `java.net.Socket`).

!!! note "FIXME Describe `pythonExec`"

`compute` [newWriterThread](#newWriterThread) with the Python worker and the input arguments.

`compute` creates and starts a [MonitorThread](../MonitorThread.md) to watch the Python worker.

`compute` [creates a new reader iterator](#newReaderIterator) to read lines from the Python worker's stdout.

---

`compute` is used when:

* `PythonRDD` is requested to [compute a partition](../PythonRDD.md#compute)
* [AggregateInPandasExec](../sql/AggregateInPandasExec.md), `ArrowEvalPythonExec`, `BatchEvalPythonExec`, `FlatMapCoGroupsInPandasExec`, `FlatMapGroupsInPandasExec` `MapInPandasExec`, `WindowInPandasExec` physical operators are executed
* `PandasGroupUtils` is requested to `executePython`
* `PythonForeachWriter` is requested for the [outputIterator](../PythonForeachWriter.md#outputIterator)
