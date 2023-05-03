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

### newReaderIterator { #newReaderIterator }

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

### newWriterThread { #newWriterThread }

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

## Computing Result { #compute }

```scala
compute(
  inputIterator: Iterator[IN],
  partitionIndex: Int,
  context: TaskContext): Iterator[OUT]
```

`compute` uses the given `TaskContext` to look up the following local properties (if they were specified via `ResourceProfile`):

* `resource.executor.cores`
* `resource.pyspark.memory`

`compute` requests the `DiskBlockManager` for the local directories and creates a comma-separated list of them (`localdir`).

Unless `spark.executorEnv.OMP_NUM_THREADS` is explicitly specified (in the [SparkConf](#conf)), `compute` sets `OMP_NUM_THREADS` (in the [envVars](#envVars)) to be the value of`resource.executor.cores` (if defined).

`compute` sets the following in the [envVars](#envVars):

* `SPARK_LOCAL_DIRS` as the local directories of the local `DiskBlockManager` (`localdir`)

`compute` can optionally define environment variables:

* `SPARK_REUSE_WORKER` as `1` when `spark.python.worker.reuse` configuration property is enabled
* `SPARK_SIMPLIFIED_TRACEBACK` as `1` when [simplifiedTraceback](#simplifiedTraceback) is enabled
* _others_

`compute` requests the executor's `SparkEnv` to `createPythonWorker` ([Spark Core]({{ book.spark_core }}/SparkEnv#createPythonWorker)) with the [pythonExec](#pythonExec) and the [envVars](#envVars).

!!! note "SparkEnv.createPythonWorker"
    When requested to create a new Python worker, `SparkEnv` creates a [PythonWorkerFactory](../PythonWorkerFactory.md) (unless already created for the `pythonExec` and the `envVars` pair) to [create a worker process](../PythonWorkerFactory.md#create).

`compute` [creates a new WriterThread](#newWriterThread) (to feed the worker process input from the given `inputIterator`) and starts it.

`compute` creates and starts a `WriterMonitorThread`.

`compute` creates a `MonitorThread`.

`compute` creates a buffered `DataInputStream` to read from the worker (socket) output. `compute` uses the [bufferSize](#bufferSize).

In the end, `compute` [creates a new ReaderIterator](#newReaderIterator) to read lines from the Python worker's stdout (from the buffered `DataInputStream`).

---

`compute` is used when:

* `PythonRDD` is requested to [compute a partition](../PythonRDD.md#compute)
* [AggregateInPandasExec](../sql/AggregateInPandasExec.md), [ArrowEvalPythonExec](../sql/ArrowEvalPythonExec.md), `BatchEvalPythonExec`, `FlatMapCoGroupsInPandasExec`, `FlatMapGroupsInPandasExec` `MapInPandasExec`, `WindowInPandasExec` physical operators are executed
* `PandasGroupUtils` is requested to `executePython`
* `PythonForeachWriter` is requested for the [outputIterator](../PythonForeachWriter.md#outputIterator)
