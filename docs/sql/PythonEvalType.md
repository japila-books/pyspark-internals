# PythonEvalType

`PythonEvalType` are the types of commands that will be sent to the Python worker.

Name | Value | PandasUDFType
-----|-------|--------------
[SQL_GROUPED_AGG_PANDAS_UDF](#SQL_GROUPED_AGG_PANDAS_UDF) | 202 | [GROUPED_AGG](../pyspark/sql/pandas/PandasUDFType.md#GROUPED_AGG)
[SQL_GROUPED_MAP_PANDAS_UDF](#SQL_GROUPED_MAP_PANDAS_UDF) | 201 | [GROUPED_MAP](../pyspark/sql/pandas/PandasUDFType.md#GROUPED_MAP)
[SQL_SCALAR_PANDAS_UDF](#SQL_SCALAR_PANDAS_UDF) | 200 | [SCALAR](../pyspark/sql/pandas/PandasUDFType.md#SCALAR)
[SQL_SCALAR_PANDAS_ITER_UDF](#SQL_SCALAR_PANDAS_ITER_UDF) | 204 | [SCALAR_ITER](../pyspark/sql/pandas/PandasUDFType.md#SCALAR_ITER)

`PythonEvalType` is defined in `org.apache.spark.api.python` Scala package with the same values defined on Python side in the [PythonEvalType](../pyspark/sql/pandas/PandasUDFType.md) Python class (in `pyspark/rdd.py` package).

## SQL_SCALAR_PANDAS_UDF { #SQL_SCALAR_PANDAS_UDF }

`SQL_SCALAR_PANDAS_UDF` is among [SCALAR_TYPES](PythonUDF.md#SCALAR_TYPES) of [PythonUDF](PythonUDF.md).

`SQL_SCALAR_PANDAS_UDF` is equivalent to [PandasUDFType.SCALAR](../pyspark/sql/pandas/PandasUDFType.md#SCALAR).

`SQL_SCALAR_PANDAS_UDF` (with [SQL_SCALAR_PANDAS_ITER_UDF](#SQL_SCALAR_PANDAS_ITER_UDF)) are evaluated using [ArrowEvalPython](ArrowEvalPython.md).

`SQL_SCALAR_PANDAS_UDF` is used (on Python side) when:

* `pyspark/worker.py` is requested to `read_single_udf` and `read_udfs`
* `UDFRegistration` is requested to [register a Python UDF](UDFRegistration.md#register)
* `UserDefinedFunction` is requested to [returnType](UserDefinedFunction.md#returnType)
* `pyspark/pandas/functions.py` is requested to `_create_pandas_udf` and `pandas_udf`

## SQL_SCALAR_PANDAS_ITER_UDF { #SQL_SCALAR_PANDAS_ITER_UDF }
