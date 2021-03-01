# udf.py

`udf.py` module belongs to `pyspark.sql` package.

## <span id="all"> Public Objects

`udf` module defines [UDFRegistration](../../UDFRegistration.md) as the public object.

## <span id="_create_udf"> _create_udf

```python
_create_udf(f, returnType, evalType)
```

`_create_udf` creates an [UserDefinedFunction](../../UserDefinedFunction.md) (with the name of the object to be the name of function `f`).

`_create_udf` is used when:

* [pandas_udf](pandas/functions.md#pandas_udf) function is used
* [udf](functions.md#udf) function is used
