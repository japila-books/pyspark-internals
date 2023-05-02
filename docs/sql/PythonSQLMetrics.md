# PythonSQLMetrics

`PythonSQLMetrics` is a collection of [SQL metrics](#performance-metrics) of the [physical operators](#implementations) in PySpark.

## Performance Metrics

### data returned from Python workers { #pythonDataReceived }

### data sent to Python workers { #pythonDataSent }

### number of output rows { #pythonNumRowsReceived }

## Implementations

* [AggregateInPandasExec](AggregateInPandasExec.md)
* [ArrowEvalPythonExec](ArrowEvalPythonExec.md)
* `BatchEvalPythonExec`
* `FlatMapCoGroupsInPandasExec`
* [FlatMapGroupsInPandasExec](FlatMapGroupsInPandasExec.md)
* `MapInBatchExec`
* `StateStoreWriter`
* `WindowInPandasExec`
