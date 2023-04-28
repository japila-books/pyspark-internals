# ArrowPythonRunner

`ArrowPythonRunner` is a [BasePythonRunner](BasePythonRunner.md) with [PythonArrowOutput](PythonArrowOutput.md).

## Creating Instance

`ArrowPythonRunner` takes the following to be created:

* <span id="funcs"> `Seq[ChainedPythonFunctions]`
* <span id="evalType"> Eval Type
* <span id="argOffsets"> Argument Offsets (`Array[Array[Int]]`)
* <span id="schema"> `Schema` ([Spark SQL]({{ book.spark_sql }}/StructType))
* <span id="timeZoneId"> TimeZone ID
* <span id="conf"> Configuration (`Map[String, String]`)

`ArrowPythonRunner` is created when [AggregateInPandasExec](../sql/AggregateInPandasExec.md), `ArrowEvalPythonExec`, `FlatMapGroupsInPandasExec`, `MapInPandasExec`, `WindowInPandasExec` physical operators are executed.
