# functions.py

`functions.py` defines [pandas_udf](#pandas_udf) for [pandas user-defined function](../../../pandas-udfs/index.md).

`functions.py` is part of `pyspark.sql.pandas` package.

```python
from pyspark.sql.functions import pandas_udf
```

## pandas_udf { #pandas_udf }

```python
pandas_udf(
  f=None,
  returnType=None,
  functionType=None)
```

`pandas_udf` creates a [pandas user-defined function](../../../pandas-udfs/index.md).

`pandas_udf` [_create_pandas_udf](#_create_pandas_udf) (possibly creating a partial function with `functools.partial` ([Python]({{ python.docs }}/library/functools.html#functools.partial)) when used as a [decorator](#pandas_udf_decorator)).

### Decorator { #pandas_udf_decorator }

`pandas_udf` can and usually is used as a Python decorator with two positional arguments for the return and function types.

```py
@pandas_udf(returnType, functionType)
```

### returnType { #pandas_udf_returnType }

`returnType` can be one of the following:

* `pyspark.sql.types.DataType`
* A DDL-formatted type string

### functionType { #pandas_udf_functionType }

`functionType` must be one the values from `PandasUDFType`:

* [SQL_SCALAR_PANDAS_UDF](../../../sql/PythonEvalType.md#SQL_SCALAR_PANDAS_UDF)
* [SQL_SCALAR_PANDAS_ITER_UDF](../../../sql/PythonEvalType.md#SQL_SCALAR_PANDAS_ITER_UDF)
* [SQL_GROUPED_MAP_PANDAS_UDF](../../../sql/PythonEvalType.md#SQL_GROUPED_MAP_PANDAS_UDF)
* [SQL_GROUPED_AGG_PANDAS_UDF](../../../sql/PythonEvalType.md#SQL_GROUPED_AGG_PANDAS_UDF)
* [SQL_MAP_PANDAS_ITER_UDF](../../../sql/PythonEvalType.md#SQL_MAP_PANDAS_ITER_UDF)
* [SQL_COGROUPED_MAP_PANDAS_UDF](../../../sql/PythonEvalType.md#SQL_COGROUPED_MAP_PANDAS_UDF)

### _create_pandas_udf { #_create_pandas_udf }

```py
_create_pandas_udf(
  f,
  returnType,
  evalType)
```

`_create_pandas_udf`...FIXME
