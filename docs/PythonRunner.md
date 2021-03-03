# PythonRunner

`PythonRunner` is a [command-line application](#main) (_process_) to launch Python applications.

`PythonRunner` executes [python](#main-pythonExec) as a subprocess and then has it connect back to the JVM to access system properties, etc.

## Arguments

`PythonRunner` requires the following command-line arguments:

1. Main python file (`pythonFile`)
1. Extra python files (`pyFiles`)
1. Application arguments

## <span id="main"> main

`main` takes the [arguments](#arguments) from command line.

<span id="main-pythonExec">
`main` determines what python executable to use based on (in that order):

1. [spark.pyspark.driver.python](configuration-properties.md#spark.pyspark.driver.python) configuration property
1. [spark.pyspark.python](configuration-properties.md#spark.pyspark.python) configuration property
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
 `PYSPARK_GATEWAY_PORT` | [getListeningPort](Py4JServer.md#getListeningPort)
 `PYSPARK_GATEWAY_SECRET` | [secret](Py4JServer.md#secret)
 `PYSPARK_PYTHON` | [spark.pyspark.python](configuration-properties.md#spark.pyspark.python) if defined
 `PYTHONHASHSEED` | `PYTHONHASHSEED` env var if defined
 `OMP_NUM_THREADS` | `spark.driver.cores` unless defined

`main` waits for the Python process to finish and requests the `Py4JServer` to [shutdown](Py4JServer.md#shutdown).

## Demo

```text
./bin/spark-class org.apache.spark.deploy.PythonRunner
```
