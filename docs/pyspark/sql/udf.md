# udf.py

`udf.py` module belongs to `pyspark.sql` package.

## <span id="all"> Public Objects

`udf` module defines [UDFRegistration](../../sql/UDFRegistration.md) as the public object.

## _create_udf { #_create_udf }

```py
_create_udf(
    f: Callable[..., Any],
    returnType: "DataTypeOrString",
    evalType: int,
    name: Optional[str] = None,
    deterministic: bool = True) -> "UserDefinedFunctionLike"
```

`_create_udf` creates an [UserDefinedFunction](UserDefinedFunction.md) (with the name of the object to be the name of function `f`).

---

`_create_udf` is used when:

* `UDFRegistration` is requested to [register](../../sql/UDFRegistration.md#register)
* [udf](functions.md#udf) is used (and [_create_py_udf](#_create_py_udf) is executed)
* [pandas_udf](pandas/functions.md#pandas_udf) (from `pyspark.sql.pandas`) is executed

## _create_py_udf { #_create_py_udf }

```py
_create_py_udf(
    f: Callable[..., Any],
    returnType: "DataTypeOrString",
    evalType: int,
) -> "UserDefinedFunctionLike"
```

`_create_py_udf`...FIXME

---

`_create_py_udf` is used when:

* [udf](functions.md#udf) is executed
