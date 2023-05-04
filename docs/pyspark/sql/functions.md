# functions.py

`functions.py` module belongs to `pyspark.sql` package.

```py
from pyspark.sql.functions import udf
```

## udf

```py
udf(
    f: Optional[Union[Callable[..., Any], "DataTypeOrString"]] = None,
    returnType: "DataTypeOrString" = StringType(),
) -> Union["UserDefinedFunctionLike", Callable[[Callable[..., Any]], "UserDefinedFunctionLike"]]
```

`udf` [_create_py_udf](udf.md#_create_py_udf) with [SQL_BATCHED_UDF](../../sql/PythonEvalType.md#SQL_BATCHED_UDF) eval type.
