# UserDefinedFunction

`UserDefinedFunction` is a Python class in [pyspark.sql.udf](udf.md) module.

```py
from pyspark.sql.udf import UserDefinedFunction
```

## Creating Instance

`UserDefinedFunction` takes the following to be created:

* <span id="func"> Function (`Callable`)
* <span id="returnType"><span id="_returnType"> Return Type (default: `StringType`)
* <span id="name"> Name (default: `None`)
* <span id="evalType"> Eval Type (default: [SQL_BATCHED_UDF](../../sql/PythonEvalType.md#SQL_BATCHED_UDF))
* <span id="deterministic"> `deterministic` flag (default: `True`)

`UserDefinedFunction` is created when:

* [_create_udf](udf.md#_create_udf) (from `pyspark.sql.udf` module) is executed

### _judf_placeholder { #_judf_placeholder }

`UserDefinedFunction` initializes `_judf_placeholder` to be `None` when [created](#creating-instance).

`_judf_placeholder` is [_create_judf](#_create_judf) of the [func](#func) when `UserDefinedFunction` is requested to [_judf](#_judf).

`_judf_placeholder` is available as [_judf](#_judf).

`_judf_placeholder` can be reset (`None`) when `UserDefinedFunction` is requested to [asNondeterministic](#asNondeterministic).

## \_\_call__

```py
__call__(
  self,
  *cols: "ColumnOrName") -> Column
```

??? note "Emulating callable objects"
    Instances of arbitrary classes can be made callable by defining a `__call__()` method in their class.

    `__call__` is called when an instance is "called" as a function.

    Learn more in [3.3.6. Emulating callable objects]({{ python.docs }}/reference/datamodel.html?#object.__call__).

With `profiler_collector` enabled, `__call__`...FIXME

Otherwise, `__call__` assigns the [_judf](#_judf) as the [judf](#judf) and creates a [PythonUDF](../../sql/PythonUDF.md).

In the end, `__call__` creates a `Column` with the `PythonUDF`.

## _judf { #_judf }

```py
@property
_judf(
  self) -> JavaObject
```

`_judf` [_create_judf](#_create_judf) for the [func](#func) unless the [_judf_placeholder](#_judf_placeholder) has already been initialized.

In the end, `_judf` returns the [_judf_placeholder](#_judf_placeholder).

---

`_judf` is used when:

* `UserDefinedFunction` is requested to [\_\_call__](#__call__)
* `UDFRegistration` is requested to [register](../../sql/UDFRegistration.md#register)

## Creating Java UserDefinedPythonFunction { #_create_judf }

```py
_create_judf(
  self,
  func: Callable[..., Any]) -> JavaObject
```

`_create_judf` uses the [_jvm](../../SparkContext.md#_jvm) bridge to create a [UserDefinedPythonFunction](../../sql/UserDefinedPythonFunction.md) with the following:

* [_name](#_name)
* [SimplePythonFunction](udf.md#_wrap_function) (with a pickled version) of the given `func` and the [returnType](#returnType)
* The [returnType](#returnType) (parsed from JSON format to Java)
* [evalType](#evalType)
* [deterministic](#deterministic)

---

`_create_judf` is used when:

* `UserDefinedFunction` is requested to [\_\_call__](#__call__) and [_judf](#_judf)
