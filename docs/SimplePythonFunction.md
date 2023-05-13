# SimplePythonFunction

`SimplePythonFunction` is a [PythonFunction](PythonFunction.md).

## Creating Instance

`SimplePythonFunction` takes the following to be created:

* <span id="command"> Command (byte array)
* <span id="envVars"> Environment Variables
* <span id="pythonIncludes"> Python Includes
* [Python Executable](#pythonExec)
* <span id="pythonVer"> Python Version
* <span id="broadcastVars"> `Broadcast`s of [PythonBroadcast](PythonBroadcast.md)s
* <span id="accumulator"> [PythonAccumulatorV2](PythonAccumulatorV2.md)

`SimplePythonFunction` is created when:

* `SparkConnectPlanner` is requested to `transformPythonFunction`
* `pyspark.rdd` (Python module) is requested to [_wrap_function](pyspark/rdd.md#_wrap_function)
* `pyspark.sql.udf` (Python module) is requested to [_wrap_function](pyspark/sql/udf.md#_wrap_function)

### Python Executable { #pythonExec }

`SimplePythonFunction` is given the **Python Executable** when [created](#creating-instance).

The Python Executable is controlled by [PYSPARK_PYTHON](environment-variables.md#PYSPARK_PYTHON) environment variable (in PySpark) or [PYSPARK_DRIVER_PYTHON](environment-variables.md#PYSPARK_DRIVER_PYTHON) (in [PySpark Connect](connect/index.md)).
