---
tags:
  - Scala
---

# PythonFunction

`PythonFunction` is an [abstraction](#contract) of the [metadata](#implementations) of a [Python function](sql/PythonUDF.md#func) of a [PythonUDF](sql/PythonUDF.md).

`PythonFunction` is executed in a [BasePythonRunner](runners/BasePythonRunner.md).

`PythonFunction` is used to create the following:

* [PythonRDD](PythonRDD.md#func)
* [PythonRunner](PythonRunner.md#apply)
* [PythonForeachWriter](PythonForeachWriter.md#func)
* [UserDefinedPythonFunction](sql/UserDefinedPythonFunction.md#func)

!!! note "ChainedPythonFunctions"
    `ChainedPythonFunctions` is a collection of chained `PythonFunction`s.

## Contract (Subset)

### accumulator

```scala
accumulator: PythonAccumulatorV2
```

[PythonAccumulatorV2](PythonAccumulatorV2.md)

Used when:

* `BasePythonRunner` is [created](runners/BasePythonRunner.md#accumulator)

### broadcastVars { #broadcastVars }

```scala
broadcastVars: JList[Broadcast[PythonBroadcast]]
```

A collection of broadcast variables ([Spark Core]({{ book.spark_core }}/broadcast-variables/Broadcast)) with a [PythonBroadcast](PythonBroadcast.md)

Used when:

* `WriterThread` is created

### command

```scala
command: Seq[Byte]
```

Used when:

* `PythonRunner` is requested to [newWriterThread](PythonRunner.md#newWriterThread)
* `UDFRegistration` is requested to [register a Python UDF](sql/UDFRegistration.md#registerPython) (for logging purposes only)
* `PythonUDFRunner` is requested to [writeUDFs](runners/PythonUDFRunner.md#writeUDFs)

## Implementations

* [SimplePythonFunction](SimplePythonFunction.md)
