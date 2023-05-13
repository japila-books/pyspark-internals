---
title: spark
---

# spark Configuration Properties

## <span id="BROADCAST_FOR_UDF_COMPRESSION_THRESHOLD"> broadcast.UDFCompressionThreshold { #spark.broadcast.UDFCompressionThreshold }

**spark.broadcast.UDFCompressionThreshold**

The threshold at which user-defined functions (UDFs) and Python RDD commands are compressed by broadcast (in bytes)

Default: `1L * 1024 * 1024` (1MB)

Used when:

* `PythonUtils` is requested to [getBroadcastThreshold](../PythonUtils.md#getBroadcastThreshold)
