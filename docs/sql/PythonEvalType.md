# PythonEvalType

`PythonEvalType` are the types of commands that will be sent to the Python worker for execution.

Name | Value | PandasUDFType
-----|-------|--------------
[SQL_GROUPED_AGG_PANDAS_UDF](#SQL_GROUPED_AGG_PANDAS_UDF) | 202 | [GROUPED_AGG](../pyspark/sql/pandas/PandasUDFType.md#GROUPED_AGG)
[SQL_GROUPED_MAP_PANDAS_UDF](#SQL_GROUPED_MAP_PANDAS_UDF) | 201 | [GROUPED_MAP](../pyspark/sql/pandas/PandasUDFType.md#GROUPED_MAP)
[SQL_SCALAR_PANDAS_UDF](#SQL_SCALAR_PANDAS_UDF) | 200 | [SCALAR](../pyspark/sql/pandas/PandasUDFType.md#SCALAR)
[SQL_SCALAR_PANDAS_ITER_UDF](#SQL_SCALAR_PANDAS_ITER_UDF) | 204 | [SCALAR_ITER](../pyspark/sql/pandas/PandasUDFType.md#SCALAR_ITER)

`PythonEvalType` is defined in `org.apache.spark.api.python` Scala package with the same values defined on Python side in the [PythonEvalType](../pyspark/sql/pandas/PandasUDFType.md) Python class (in `pyspark/rdd.py` package).

## SQL_GROUPED_AGG_PANDAS_UDF { #SQL_GROUPED_AGG_PANDAS_UDF }

`SQL_GROUPED_AGG_PANDAS_UDF` is a UDF marker of **Grouped Aggregate Pandas UDFs** (_pandas User-Defined Aggregate Functions_, _pandas UDAFs_).

`SQL_GROUPED_AGG_PANDAS_UDF` is executed using [AggregateInPandasExec](AggregateInPandasExec.md) physical operator (using [ArrowPythonRunner](../runners/ArrowPythonRunner.md)).

Limitations of Pandas UDAFs:

* [Return type](../pyspark/sql/UserDefinedFunction.md#returnType) cannot be `StructType`
* Not supported in the `PIVOT` clause
* Not supported in streaming aggregation

`SQL_GROUPED_AGG_PANDAS_UDF` is used (on Python side) when:

* `pyspark/worker.py` is requested to [read_single_udf](../pyspark/worker.md#read_single_udf) and [read_udfs](../pyspark/worker.md#read_udfs)
* `pyspark/sql/pandas/functions.py` is requested to `_create_pandas_udf` and `pandas_udf`

`SQL_GROUPED_AGG_PANDAS_UDF` is used (on Scala side) when:

* `PythonUDF` is requested for [isGroupedAggPandasUDF](PythonUDF.md#isGroupedAggPandasUDF)

## SQL_SCALAR_PANDAS_UDF { #SQL_SCALAR_PANDAS_UDF }

`SQL_SCALAR_PANDAS_UDF` is among [SCALAR_TYPES](PythonUDF.md#SCALAR_TYPES) of [PythonUDF](PythonUDF.md).

`SQL_SCALAR_PANDAS_UDF` (with [SQL_SCALAR_PANDAS_ITER_UDF](#SQL_SCALAR_PANDAS_ITER_UDF)) are evaluated using [ArrowEvalPython](ArrowEvalPython.md).

`SQL_SCALAR_PANDAS_UDF` is used (on Python side) when:

* `pyspark/worker.py` is requested to [read_single_udf](../pyspark/worker.md#read_single_udf) and [read_udfs](../pyspark/worker.md#read_udfs)
* `pyspark/sql/pandas/functions.py` is requested to `_create_pandas_udf` and `pandas_udf`

## SQL_SCALAR_PANDAS_ITER_UDF { #SQL_SCALAR_PANDAS_ITER_UDF }

## User-Defined Functions

[UDFRegistration](UDFRegistration.md#register) allows user-defined functions to be one of the following `PythonEvalType`s:

* [SQL_BATCHED_UDF](#SQL_BATCHED_UDF)
* [SQL_SCALAR_PANDAS_UDF](#SQL_SCALAR_PANDAS_UDF)
* [SQL_SCALAR_PANDAS_ITER_UDF](#SQL_SCALAR_PANDAS_ITER_UDF)
* [SQL_GROUPED_AGG_PANDAS_UDF](#SQL_GROUPED_AGG_PANDAS_UDF)
