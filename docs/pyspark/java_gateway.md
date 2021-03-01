# java_gateway.py

`java_gateway` Python module allows for [launching a gateway process](#launch_gateway) to establish communication channel between this and [Py4JServer](../Py4JServer.md).

## <span id="launch_gateway"> launch_gateway

```python
launch_gateway(
  conf=None,
  popen_kwargs=None)
```

`launch_gateway` reads `PYSPARK_GATEWAY_PORT` and `PYSPARK_GATEWAY_SECRET` environment variables if defined and assumes that the child Java gateway process has already been started (e.g. [PythonGatewayServer](../PythonGatewayServer.md)).

<span id="launch_gateway-command">

Otherwise, `launch_gateway` builds the command to start `spark-submit`:

1. Finds `SPARK_HOME` with `./bin/spark-submit`
1. Appends all the configuration properties (from the input `conf`) using `--conf`
1. Appends `PYSPARK_SUBMIT_ARGS` environment variable if defined or assumes `pyspark-shell`

`launch_gateway` sets up `_PYSPARK_DRIVER_CONN_INFO_PATH` environment variable to point at an unique temporary file.

`launch_gateway` configures a pipe to stdin for the corresponding Java gateway process to use to monitor the Python process.

`launch_gateway` starts `bin/spark-submit` command and waits for a connection info file to be created at `_PYSPARK_DRIVER_CONN_INFO_PATH`. `launch_gateway` reads the port and the secret from the file once available.

`launch_gateway` connects to the gateway using py4j's `ClientServer` or `JavaGateway` based on `PYSPARK_PIN_THREAD` environment variable (default: `false`).

PYSPARK_PIN_THREAD | Gateway
-------------------|----------
 `true`            | `ClientServer`
 `false`           | `JavaGateway`

`launch_gateway` imports Spark packages and classes (using py4j):

* `org.apache.spark.SparkConf`
* `org.apache.spark.api.java.*`
* `org.apache.spark.api.python.*`
* `org.apache.spark.ml.python.*`
* `org.apache.spark.mllib.api.python.*`
* `org.apache.spark.resource.*`
* `org.apache.spark.sql.*`
* `org.apache.spark.sql.api.python.*`
* `org.apache.spark.sql.hive.*`
* `scala.Tuple2`

`launch_gateway` is used when:

* `SparkContext` is requested to [_ensure_initialized](../SparkContext.md#_ensure_initialized)
