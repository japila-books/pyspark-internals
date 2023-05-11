# SparkEnv

!!! note "Learn More"
    This is a stub for [pythonWorkers](#pythonWorkers) et al.
    Learn more in [The Internals of Apache Spark]({{ book.spark_core }}/SparkEnv/).

## pythonWorkers Registry { #pythonWorkers }

```scala
pythonWorkers: Map[(String, Map[String, String]), PythonWorkerFactory]
```

`SparkEnv` creates an empty collection of [PythonWorkerFactory](PythonWorkerFactory.md)s (by their `pythonExec` and the `envVars`) when created.

A new `PythonWorkerFactory` is created in [createPythonWorker](#createPythonWorker) when there was no `PythonWorkerFactory` for a `pythonExec` and a `envVars` pair.

All `PythonWorkerFactory`s are requested to [stop](PythonWorkerFactory.md#stop) when `SparkEnv` is requested to `stop`.

`pythonWorkers` is used in [destroyPythonWorker](#destroyPythonWorker) and [releasePythonWorker](#releasePythonWorker).

## Looking Up or Creating Python Worker Process { #createPythonWorker }

```scala
createPythonWorker(
  pythonExec: String,
  envVars: Map[String, String]): (java.net.Socket, Option[Int])
```

`createPythonWorker` looks up a [PythonWorkerFactory](PythonWorkerFactory.md) (in [pythonWorkers](#pythonWorkers)) for the given `pythonExec` and the `envVars` pair. Unless found, `createPythonWorker` registers a new `PythonWorkerFactory`.

In the end, `createPythonWorker` requests the `PythonWorkerFactory` to [create a Python worker process](PythonWorkerFactory.md#create).

---

``createPythonWorker`` is used when:

* `BasePythonRunner` is requested to [compute a partition](runners/BasePythonRunner.md#compute)
