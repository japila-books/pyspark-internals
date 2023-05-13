# rdd.py

`rdd` module (in `pyspark` package) defines [RDD](../RDD.md).

```py
from pyspark.rdd import *
```

## \_\_all__

??? note "import *"
    The `import` statement uses the following convention: if a package’s `__init__.py` code defines a list named `__all__`, it is taken to be the list of module names that should be imported when `from package import *` is encountered.

    Learn more in [6.4.1. Importing * From a Package]({{ python.docs }}/tutorial/modules.html#importing-from-a-package).

* [RDD](../RDD.md)

## _prepare_for_python_RDD { #_prepare_for_python_RDD }

```py
_prepare_for_python_RDD(
  sc: "SparkContext",
  command: Any) -> Tuple[bytes, Any, Any, Any]
```

`_prepare_for_python_RDD` creates a `CloudPickleSerializer` to `dumps` the given `command` pair (that creates a `pickled_command`).

If the size of the `pickled_command` is above the [broadcast threshold](../PythonUtils.md#getBroadcastThreshold), `_prepare_for_python_RDD` creates a broadcast variable for `pickled_command` that is in turn `dumps` using the `CloudPickleSerializer` (that overrides the `pickled_command`).

In the end, `_prepare_for_python_RDD` returns the following:

* `pickled_command`
* `broadcast_vars`
* [environment](../SparkContext.md#environment)
* [_python_includes](../SparkContext.md#_python_includes)

---

`_prepare_for_python_RDD` is used when:

* `pyspark.rdd` is requested to [_wrap_function](#_wrap_function)
* `pyspark.sql.udf` is requested to [_wrap_function](sql/udf.md#_wrap_function)
