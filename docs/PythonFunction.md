# PythonFunction

`PythonFunction` is a metadata of a Python function to be executed in [PythonRunner](PythonRunner.md).

## Creating Instance

`PythonFunction` takes the following to be created:

* <span id="command"> Command (`Array[Byte]`)
* <span id="envVars"> Environment Variables (`Map[String, String]`)
* <span id="pythonIncludes"> Python Includes (`List[String]`)
* <span id="pythonExec"> Python Executable
* <span id="pythonVer"> Python Version
* <span id="broadcastVars"> Broadcast Variables with [PythonBroadcast](PythonBroadcast.md)]s
* <span id="accumulator"> [PythonAccumulatorV2](PythonAccumulatorV2.md)

`PythonFunction` is created when...FIXME
