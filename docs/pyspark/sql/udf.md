# udf.py

`udf` module (in `pyspark.sql` package) defines [UDFRegistration](../../sql/UDFRegistration.md).

```py
from pyspark.sql.udf import *
```

## \_\_all__

??? note "import *"
    The `import` statement uses the following convention: if a package’s `__init__.py` code defines a list named `__all__`, it is taken to be the list of module names that should be imported when `from package import *` is encountered.

    Learn more in [6.4.1. Importing * From a Package]({{ python.docs }}/tutorial/modules.html#importing-from-a-package).

* [UDFRegistration](../../sql/UDFRegistration.md)

## _create_udf { #_create_udf }

```py
_create_udf(
    f: Callable[..., Any],
    returnType: "DataTypeOrString",
    evalType: int,
    name: Optional[str] = None,
    deterministic: bool = True) -> "UserDefinedFunctionLike"
```

`_create_udf` creates a [UserDefinedFunction](UserDefinedFunction.md) (with the name of the object to be the name of function `f`).

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

## Creating SimplePythonFunction for (Pickled) Python Function { #_wrap_function }

```py
_wrap_function(
  sc: SparkContext,
  func: Callable[..., Any],
  returnType: "DataTypeOrString") -> JavaObject
```

`_wrap_function` creates a `command` tuple with the given `func` and `returnType`.

`_wrap_function` [_prepare_for_python_RDD](../rdd.md#_prepare_for_python_RDD) for the `command` tuple that builds the input for a [SimplePythonFunction](../../SimplePythonFunction.md):

* `pickled_command` byte array
* `env`
* `includes`
* `broadcast_vars`

In the end, `_wrap_function` creates a [SimplePythonFunction](../../SimplePythonFunction.md) with the above and the following from the given [SparkContext](../../SparkContext.md):

* [pythonExec](../../SparkContext.md#pythonExec)
* [pythonVer](../../SparkContext.md#pythonVer)
* [_javaAccumulator](../../SparkContext.md#_javaAccumulator)

---

`_wrap_function` is used when:

* `UserDefinedFunction` is requested to [_create_judf](UserDefinedFunction.md#_create_judf)
