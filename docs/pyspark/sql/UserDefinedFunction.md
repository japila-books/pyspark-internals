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

## _create_judf { #_create_judf }

```py
_create_judf(
  self,
  func: Callable[..., Any]) -> JavaObject
```

`_create_judf` uses the [_jvm](../../SparkContext.md#_jvm) bridge to create a [UserDefinedPythonFunction](../../sql/UserDefinedPythonFunction.md) with the following:

* [_name](#_name)
* [Wrapped](#_wrap_function) the given `func` (and the [returnType](#returnType))
* The [returnType](#returnType) (parsed from JSON format to Java)
* [evalType](#evalType)
* [deterministic](#deterministic)
