# PythonGatewayServer

`PythonGatewayServer` is a [standalone application](#main) (_process_) that starts a [Py4JServer](Py4JServer.md) on an ephemeral port.

`PythonGatewayServer` is the Python runner for `pyspark` shell ([Apache Spark]({{ book.spark_core }}/tools/SparkSubmit#PYSPARK_SHELL)).

## <span id="main"> main

```scala
main(
  args: Array[String]): Unit
```

`main` creates a [Py4JServer](Py4JServer.md) and requests it to [start](Py4JServer.md#start).

`main` requests the `Py4JServer` for the [listening port](Py4JServer.md#getListeningPort) (_boundPort_) and prints out the following DEBUG message to the logs:

```text
Started PythonGatewayServer on port [boundPort]
```

<span id="main-_PYSPARK_DRIVER_CONN_INFO_PATH">
`main` uses [_PYSPARK_DRIVER_CONN_INFO_PATH](#_PYSPARK_DRIVER_CONN_INFO_PATH) environment variable for the path of a connection info file (for the associated python process) with the listening port and the [secret](Py4JServer.md#secret).

`main` pauses (_blocks_) until the Python driver finishes (by reading from the system input that blocks until input data is available, the end of the stream is detected, or an exception is thrown).

In the end, once the Python driver finishes, `main` prints out the following DEBUG message to the logs:

```text
Exiting due to broken pipe from Python driver
```

`main` prints out the following ERROR message to the logs and exists when the [listening port](Py4JServer.md#getListeningPort) is `-1`:

```text
[server] failed to bind; exiting
```

## <span id="_PYSPARK_DRIVER_CONN_INFO_PATH"> _PYSPARK_DRIVER_CONN_INFO_PATH

`PythonGatewayServer` uses `_PYSPARK_DRIVER_CONN_INFO_PATH` environment variable for the [path of a connection info file](#main-_PYSPARK_DRIVER_CONN_INFO_PATH) for communication between this and the Python processes.

`_PYSPARK_DRIVER_CONN_INFO_PATH` is configured when [java_gateway.py](pyspark/java_gateway.md) module is requested to [launch_gateway](pyspark/java_gateway.md#launch_gateway).

## Logging

Enable `ALL` logging level for `org.apache.spark.api.python.PythonGatewayServer` logger to see what happens inside.

Add the following line to `conf/log4j.properties`:

```text
log4j.logger.org.apache.spark.api.python.PythonGatewayServer=ALL
```

Refer to [Logging](spark-logging.md).
