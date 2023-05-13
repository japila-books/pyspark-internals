---
title: spark.python
---

# spark.python Configuration Properties

## <span id="PYTHON_DAEMON_MODULE"> daemon.module { #spark.python.daemon.module }

**spark.python.daemon.module**

The Python module to run the daemon to execute Python workers

Default: [pyspark.daemon](../pyspark/daemon.md)

Used when:

* `PythonWorkerFactory` is [created](../PythonWorkerFactory.md#daemonModule)

## <span id="PYTHON_USE_DAEMON"> use.daemon { #spark.python.use.daemon }

**spark.python.use.daemon**

Because forking processes from Java is expensive, PySpark prefers launching a single Python daemon ([spark.python.daemon.module](#spark.python.daemon.module)) to fork new workers for tasks.
This daemon currently only works on UNIX-based systems now because it uses signals for child management, so we can also fall back to launching workers ([spark.python.worker.module](#spark.python.worker.module)) directly.

Default: `true` (unless PySpark runs on Windows)

Used when:

* `PythonWorkerFactory` is [created](../PythonWorkerFactory.md#useDaemon)

## <span id="PYTHON_WORKER_MODULE"> worker.module { #spark.python.worker.module }

**spark.python.worker.module**

The Python module to run a Python worker

Default: [pyspark.worker](../pyspark/worker.md)

Used when:

* `PythonWorkerFactory` is [created](../PythonWorkerFactory.md#workerModule)
