# PythonUtils

## Broadcast Threshold { #getBroadcastThreshold }

```scala
getBroadcastThreshold(
  sc: JavaSparkContext): Long
```

`getBroadcastThreshold` is the value of [spark.broadcast.UDFCompressionThreshold](configuration-properties/spark.md#spark.broadcast.UDFCompressionThreshold) configuration property.

!!! note "py4j"
    `getBroadcastThreshold` is a Scala method that is used by [pyspark.rdd](pyspark/rdd.md#_prepare_for_python_RDD) Python module via [py4j](SparkContext.md#_jvm) bridge.

---

`getBroadcastThreshold` is used when:

* `pyspark.rdd` is requested to [_prepare_for_python_RDD](pyspark/rdd.md#_prepare_for_python_RDD)
