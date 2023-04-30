# PandasUDFType

!!! warning "Deprecation Notice"
    As of [PySpark 3.0.0](https://issues.apache.org/jira/browse/SPARK-28264), `PandasUDFType` is deprecated in favour of Python type hints.

`PandasUDFType` is the `functionType` of [pandas_udf](../../../pandas-udfs/index.md#pandas_udf) for Python methods to be used as [pandas UDFs](../../../pandas-udfs/index.md) (with the types matching [PythonEvalType](../../../sql/PythonEvalType.md) on the JVM/Scala side).

PandasUDFType | PythonEvalType
--------------|---------------
 `GROUPED_AGG` | [SQL_GROUPED_AGG_PANDAS_UDF](../../../sql/PythonEvalType.md#SQL_GROUPED_AGG_PANDAS_UDF)
 `GROUPED_MAP` | [SQL_GROUPED_MAP_PANDAS_UDF](../../../sql/PythonEvalType.md#SQL_GROUPED_MAP_PANDAS_UDF)
 `SCALAR` | [SQL_SCALAR_PANDAS_UDF](../../../sql/PythonEvalType.md#SQL_SCALAR_PANDAS_UDF)
 `SCALAR_ITER` | [SQL_SCALAR_PANDAS_ITER_UDF](../../../sql/PythonEvalType.md#SQL_SCALAR_PANDAS_ITER_UDF)
