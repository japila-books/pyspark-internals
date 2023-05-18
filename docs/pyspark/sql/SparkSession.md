# SparkSession

`SparkSession` is a Python class in [pyspark.sql.session](session.md) module.

```py
from pyspark.sql.session import SparkSession
```

## SparkConversionMixin { #SparkConversionMixin }

`SparkSession` uses [SparkConversionMixin](../../sql/SparkConversionMixin.md) (for pandas to Spark conversion).

## Creating Instance

`SparkSession` takes the following to be created:

* <span id="sparkContext"><span id="_sc"> [SparkContext](../../SparkContext.md)
* <span id="jsparkSession"> `SparkSession` (`Optional[JavaObject]`)
* <span id="options"> Options

While being created, `SparkSession` gets access to [_jsc](#_jsc) and [_jvm](#_jvm) using the given [SparkContext](#_sc).

!!! note
    It is expected that [_jvm](../../SparkContext.md#_jvm) is defined (or an exception is thrown).

Unless the given [SparkSession](#jsparkSession) is defined, `SparkSession` gets one from the [_jvm](../../SparkContext.md#_jvm).

`SparkSession` [_monkey_patch_RDD](#_monkey_patch_RDD).

`SparkSession` [install_exception_handler](#install_exception_handler).

---

`SparkSession` is created when:

* `SparkSession.Builder` is requested to [get or create one](SparkSession.Builder.md#getOrCreate)
* `SparkSession` is requested to [get an active SparkSession](#getActiveSession)

### Java SparkContext { #_jsc }

```py
_jsc: JavaObject
```

`_jsc` is a Java `SparkContext` ([Spark Core]({{ book.spark_core }}/SparkContext)) that is created through Py4J.

??? note "JavaObject"
    `JavaObject` ([Py4J]({{ py4j.docs }}/py4j_java_gateway.html#javaobject)) represents a Java object from which you can call methods or access fields.

`_jsc` is initialized when `SparkSession` is [created](#creating-instance) to be the [_jsc](../../SparkContext.md#_jsc) of the given [SparkContext](#_sc).

`_jsc` is used (among the other internal uses) when:

* `SCCallSiteSync` is requested to `__enter__` and `__exit__`

### py4j JVMView { #_jvm }

```py
_jvm: ClassVar[Optional[JVMView]]
```

??? note "JVMView"
    `JVMView` ([Py4J]({{ py4j.docs }}/py4j_java_gateway.html#jvmview)) that allows access to the Java Virtual Machine of a `JavaGateway`.

    `JVMView` can be used to reference static members (fields and methods) and to call constructors.

    From [py4j.JVMView]({{ py4j.javadoc }}/py4j/JVMView.html) javadoc:

    > A JVM view keeps track of imports and import searches. A Python client can have multiple JVM views (e.g., one for each module) so that imports in one view do not conflict with imports from other views.

`_jvm` is initialized when `SparkSession` is [created](#creating-instance) to be the [_jvm](../../SparkContext.md#_jvm) of the given [SparkContext](#_sc).

`_jvm` must be defined when `SparkSession` is [created](#creating-instance) or an `AssertionError` is thrown.

`_jvm` is "cleared" (_stopped_) in [stop](#stop).

`_jvm` is used (among the other internal uses) when:

* `ChannelBuilder` is requested to `default_port`
* `InternalFrame` is requested to `attach_distributed_column`
* `DataFrameReader` is requested to `csv` and `json`
* `pyspark.pandas.spark.functions.py` module is requested to `_call_udf` and `_make_arguments`
* `SparkConversionMixin` is requested to [_create_from_pandas_with_arrow](../../sql/SparkConversionMixin.md#_create_from_pandas_with_arrow)
* `SparkSession` is requested to [_create_dataframe](#_create_dataframe)

```text
>>> type(spark)
<class 'pyspark.sql.session.SparkSession'>

>>> type(spark._jvm)
<class 'py4j.java_gateway.JVMView'>
```

## Creating Builder { #builder }

```py
@classproperty
builder(
  cls) -> Builder
```

??? note "`@classproperty` Decorator"
    `builder` is a `@classproperty` that is PySpark-specific to mimic how [@classmethod]({{ python.docs }}/library/functions.html#classmethod) and [@property]({{ python.docs }}/library/functions.html#property) should work together.

`builder` creates a new [SparkSession.Builder](SparkSession.Builder.md).

## \_\_enter__

```py
__enter__(
  self) -> "SparkSession"
```

??? note "Special Method"
    Enables `with SparkSession.builder.(...).getOrCreate() as session:` syntax.

    Learn more:

    1. [PEP 343 – The "with" Statement]({{ python.peps }}/pep-0343/)
    1. [3.3.9. With Statement Context Managers]({{ python.docs }}/reference/datamodel.html#with-statement-context-managers)
    1. [Context Managers and Python's with Statement]({{ python.realpython }}/python-with-statement/)

`__enter__` returns `self`.

## \_\_exit__

```py
__exit__(
  self,
  exc_type: Optional[Type[BaseException]],
  exc_val: Optional[BaseException],
  exc_tb: Optional[TracebackType],
) -> None
```

??? note "Special Method"
    Enables `with SparkSession.builder.(...).getOrCreate() as session:` syntax.

    Learn more:

    1. [PEP 343 – The "with" Statement]({{ python.peps }}/pep-0343/)
    1. [3.3.9. With Statement Context Managers]({{ python.docs }}/reference/datamodel.html#with-statement-context-managers)
    1. [Context Managers and Python's with Statement]({{ python.realpython }}/python-with-statement/)

`__exit__` [stop](#stop) this `SparkSession` (which is exactly what `__exit__` is supposed to do with resource manager once they're out of scope and resources should be released).

## _create_shell_session { #_create_shell_session }

```py
@staticmethod
_create_shell_session() -> "SparkSession"
```

??? note "`@staticmethod`"
    Learn more in [Python Documentation]({{ python.docs }}/library/functions.html#staticmethod).

`_create_shell_session`...FIXME

---

`_create_shell_session` is used when:

* [pyspark/shell.py](../shell.md) module is imported

## Executing SQL Statement { #sql }

```py
sql(
  self,
  sqlQuery: str,
  args: Optional[Dict[str, Any]] = None,
  **kwargs: Any) -> DataFrame
```

`sql` creates a [DataFrame](../../sql/DataFrame.md) with the `sqlQuery` query executed.

`sql` uses `SQLStringFormatter` to `format` the given `sqlQuery` with the `kwargs`, if defined.
