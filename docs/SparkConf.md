# SparkConf

`SparkConf` is a Python class.

## Creating Instance

`SparkConf` takes the following to be created:

* <span id="loadDefaults"> `loadDefaults` flag (default: `True`)
* <span id="_jvm"> `JVMView` ([py4j]({{ py4j.doc }}/py4j_java_gateway.html#jvmview))
* <span id="_jconf"> JConf (default: `None`)

While being created, `SparkConf` uses the [JVMView](SparkContext.md#_jvm) (of the [SparkContext](SparkContext.md)) unless the `_jconf` and `_jvm` are given.

## Demo

```python
from pyspark import SparkConf
```
