# PythonRunner

`PythonRunner` is a [command-line application](#main) that is launched to run Python applications on Apache Spark using `spark-submit` shell script ([Spark Core]({{ book.spark_core }}/tools/spark-submit/)).

`PythonRunner` is used by [spark-submit](demo/executing-pyspark-applications-using-spark-submit.md).

`PythonRunner` executes a configured [python executable](#main-pythonExec) as a subprocess that is supposed to connect back to the JVM to access Spark services.

## Arguments

`PythonRunner` requires the following command-line arguments:

1. Main python file (`pythonFile`)
1. Extra python files (`pyFiles`)
1. Application arguments

## main

`main` takes the [arguments](#arguments) from command line.

<span id="main-pythonExec">
`main` determines what python executable to use based on (in that order):

1. [spark.pyspark.driver.python](configuration-properties/index.md#spark.pyspark.driver.python) configuration property
1. [spark.pyspark.python](configuration-properties/index.md#spark.pyspark.python) configuration property
1. `PYSPARK_DRIVER_PYTHON` environment variable
1. `PYSPARK_PYTHON` environment variable
1. `python3`

`main` creates a [Py4JServer](Py4JServer.md) that is [started](Py4JServer.md#start) on a daemon **py4j-gateway-init** thread.

`main` waits until the gateway server has started.

`main` launches a Python process using the [python executable](#main-pythonExec) and the following environment variables.

Environment Variable | Value
---------------------|---------
 `PYTHONPATH` |
 `PYTHONUNBUFFERED` | YES
 [PYSPARK_GATEWAY_PORT](environment-variables.md#PYSPARK_GATEWAY_PORT) | [getListeningPort](Py4JServer.md#getListeningPort)
 [PYSPARK_GATEWAY_SECRET](environment-variables.md#PYSPARK_GATEWAY_SECRET) | [secret](Py4JServer.md#secret)
 `PYSPARK_PYTHON` | [spark.pyspark.python](configuration-properties/index.md#spark.pyspark.python) if defined
 `PYTHONHASHSEED` | `PYTHONHASHSEED` env var if defined
 `OMP_NUM_THREADS` | `spark.driver.cores` unless defined

`main` waits for the Python process to finish and requests the `Py4JServer` to [shutdown](Py4JServer.md#shutdown).
