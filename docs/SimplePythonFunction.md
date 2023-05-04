# SimplePythonFunction

`SimplePythonFunction` is a [PythonFunction](PythonFunction.md).

## Creating Instance

`SimplePythonFunction` takes the following to be created:

* <span id="command"> Command
* <span id="envVars"> Environment Variables
* <span id="pythonIncludes"> Python Includes
* <span id="pythonExec"> Python Executable
* <span id="pythonVer"> Python Version
* <span id="broadcastVars"> `Broadcast`s of [PythonBroadcast](PythonBroadcast.md)s
* <span id="accumulator"> [PythonAccumulatorV2](PythonAccumulatorV2.md)

`SimplePythonFunction` is created when:

* `SparkConnectPlanner` is requested to `transformPythonFunction`
