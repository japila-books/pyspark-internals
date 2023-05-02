# Configuration Properties

## <span id="spark.pyspark.driver.python"><span id="PYSPARK_DRIVER_PYTHON"> spark.pyspark.driver.python

Default: (undefined)

## <span id="spark.pyspark.python"><span id="PYSPARK_PYTHON"> spark.pyspark.python

Default: (undefined)

## <span id="spark.python.use.daemon"><span id="PYTHON_USE_DAEMON"> spark.python.use.daemon

Because forking processes from Java is expensive, we prefer to launch a single Python daemon, `pyspark/daemon.py` (by default) and tell it to fork new workers for our tasks. This daemon currently only works on UNIX-based systems now because it uses signals for child management, so we can also fall back to launching workers, `pyspark/worker.py` (by default) directly.

Default: `true` (always disabled on Windows)

Used when [PythonWorkerFactory](PythonWorkerFactory.md#useDaemon) is created

## <span id="spark.python.daemon.module"><span id="PYTHON_DAEMON_MODULE"> spark.python.daemon.module

Default: `pyspark.daemon`

Used when [PythonWorkerFactory](PythonWorkerFactory.md#daemonModule) is created

## <span id="spark.python.worker.module"><span id="PYTHON_WORKER_MODULE"> spark.python.worker.module

Default: (undefined)

Used when [PythonWorkerFactory](PythonWorkerFactory.md#workerModule) is created

## spark.sql.execution { #spark.sql.execution }

### <span id="ARROW_EXECUTION_MAX_RECORDS_PER_BATCH"><span id="arrowMaxRecordsPerBatch"> arrow.maxRecordsPerBatch { #spark.sql.execution.arrow.maxRecordsPerBatch }

**spark.sql.execution.arrow.maxRecordsPerBatch**

When using Apache Arrow, the maximum number of records that can be written to a single `ArrowRecordBatch` in memory.

If zero or negative there is no limit.

Default: `10000`

Used when:

* `ApplyInPandasWithStatePythonRunner` is requested for `workerConf`
* `ArrowEvalPythonExec` is [created](sql/ArrowEvalPythonExec.md#batchSize)
* `Dataset` is requested to `toArrowBatchRdd`
* `MapInBatchExec` is created
* `SparkConnectPlanner` is requested to `handleSqlCommand`
* `SparkConnectStreamHandler` is requested to `processAsArrowBatches`

### <span id="ARROW_PYSPARK_EXECUTION_ENABLED"><span id="arrowPySparkEnabled"> arrow.pyspark.enabled { #spark.sql.execution.arrow.pyspark.enabled }

**spark.sql.execution.arrow.pyspark.enabled**

Enables [Arrow Optimization](arrow-optimization/index.md)

Default: `false`

### <span id="PANDAS_UDF_BUFFER_SIZE"><span id="pandasUDFBufferSize"> pandas.udf.buffer.size { #spark.sql.execution.pandas.udf.buffer.size }

**spark.sql.execution.pandas.udf.buffer.size**

`spark.buffer.size` for Pandas UDF executions

Note that Pandas execution requires more than 4 bytes.
Lowering this value could make small Pandas UDF batch iterated and pipelined; however, it might degrade performance.
See SPARK-27870.

Default: `spark.buffer.size` ([Spark Core]({{ book.spark_core }}/configuration-properties/#spark.buffer.size))

Used when:

* `ApplyInPandasWithStatePythonRunner` and [ArrowPythonRunner](runners/ArrowPythonRunner.md#bufferSize) are created (and initialize [bufferSize](runners/BasePythonRunner.md#bufferSize))

## spark.sql.execution.pyspark { #spark.sql.execution.pyspark }

### <span id="PYSPARK_SIMPLIFIEID_TRACEBACK"><span id="pysparkSimplifiedTraceback"> udf.simplifiedTraceback.enabled { #spark.sql.execution.pyspark.udf.simplifiedTraceback.enabled }

**spark.sql.execution.pyspark.udf.simplifiedTraceback.enabled**

Controls the traceback from Python UDFs. When enabled (`true`), traceback is simplified and hides the Python worker, (de)serialization, etc. from PySpark in tracebacks, and only shows the exception messages from UDFs.

Works only with CPython 3.7+

Default: `true`

Used when:

* `ApplyInPandasWithStatePythonRunner`, [ArrowPythonRunner](runners/ArrowPythonRunner.md#simplifiedTraceback), `CoGroupedArrowPythonRunner`, [PythonUDFRunner](runners/PythonUDFRunner.md#simplifiedTraceback) are created (and initialize [simplifiedTraceback](runners/BasePythonRunner.md#simplifiedTraceback) flag)
