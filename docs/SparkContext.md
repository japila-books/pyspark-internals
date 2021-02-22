# SparkContext

`SparkContext` is a Python class.

## <span id="_gateway"> JavaGateway

`SparkContext` defines `_gateway` property for a `JavaGateway` that is given or launched when [_ensure_initialized](#_ensure_initialized).

## <span id="_jvm"> JVMView

`SparkContext` defines `_jvm` property for a `JVMView` ([py4j]({{ py4j.doc }}/py4j_java_gateway.html#jvmview)) to access to the Java Virtual Machine of the [JavaGateway](#_gateway).

## <span id="_ensure_initialized"> _ensure_initialized

```python
_ensure_initialized(
  cls, instance=None,
  gateway=None,
  conf=None)
```

`_ensure_initialized` is a `@classmethod`.

`_ensure_initialized`...FIXME

`_ensure_initialized` is used when:

* `SparkContext` is `__init__` and `setSystemProperty`
* [pyspark/shell.py](shell.md) is launched
