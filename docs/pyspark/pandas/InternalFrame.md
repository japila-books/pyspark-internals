# InternalFrame

`InternalFrame` is the underlying managed Spark DataFrame of [pyspark.pandas.DataFrame](DataFrame.md#_internal).

## Creating Instance

`InternalFrame` takes the following to be created:

* [Spark DataFrame](#spark_frame)
* <span id="index_spark_columns"> `index_spark_columns` (optional)
* <span id="index_names"> `index_names` (optional)
* <span id="index_fields"> `index_fields` (optional)
* <span id="column_labels"> `column_labels` (optional)
* <span id="data_spark_columns"> `data_spark_columns` (optional)
* <span id="data_fields"> `data_fields` (optional)
* <span id="column_label_names"> `column_label_names` (optional)

### Spark DataFrame { #spark_frame }

`InternalFrame` is given a Spark [DataFrame](../../sql/DataFrame.md) when [created](#creating-instance).

## Managed Spark DataFrame { #_sdf }

`_sdf` is the underlying managed Spark DataFrame.

`_sdf` is the [Spark DataFrame](#spark_frame) with [attach_default_index](#attach_default_index) and [\_\_natural_order__](#NATURAL_ORDER_COLUMN_NAME) columns selected.

## Default Index Column Name { #SPARK_DEFAULT_INDEX_NAME }

`InternalFrame` uses the following as the name of the default index column:

```text
__index_level_0__
```

## Index Column Pattern { #SPARK_INDEX_NAME_PATTERN }

`InternalFrame` defines a regular pattern to match the index columns.

```text
__index_level_[0-9]+__
```

It is invalid to name columns in the [Spark DataFrame](#spark_frame) to match the index column pattern.
Index columns must not be in the columns of the Spark DataFrame.

## to_internal_spark_frame { #to_internal_spark_frame }

```py
@lazy_property
def to_internal_spark_frame(
    self) -> SparkDataFrame
```

`to_internal_spark_frame` returns the [spark_frame](#spark_frame) with the [index_spark_columns](#index_spark_columns) followed by the [data_spark_columns](#data_spark_columns).

## spark_frame { #spark_frame }

```py
from pyspark.sql import DataFrame as SparkDataFrame

@property
def spark_frame(
    self) -> SparkDataFrame
```

`spark_frame` returns the underlying [managed Spark DataFrame](#_sdf).

## Demo

```py
from pyspark import pandas as ps

psdf = ps.DataFrame({
    'A': [1, 2, 3, 4],
    'B': [5, 6, 7, 8],
    'C': [9, 10, 11, 12],
    'D': [13, 14, 15, 16],
    'E': [17, 18, 19, 20]}, columns = ['A', 'B', 'C', 'D', 'E'])

psdf._internal
# <pyspark.pandas.internal.InternalFrame object at 0x7f7ff024f820>

psdf._internal.spark_frame
# DataFrame[__index_level_0__: bigint, A: bigint, B: bigint, C: bigint, D: bigint, E: bigint, __natural_order__: bigint]

psdf._internal.spark_frame.show()
# +-----------------+---+---+---+---+---+-----------------+
# |__index_level_0__|  A|  B|  C|  D|  E|__natural_order__|
# +-----------------+---+---+---+---+---+-----------------+
# |                0|  1|  5|  9| 13| 17|      17179869184|
# |                1|  2|  6| 10| 14| 18|      42949672960|
# |                2|  3|  7| 11| 15| 19|      68719476736|
# |                3|  4|  8| 12| 16| 20|      94489280512|
# +-----------------+---+---+---+---+---+-----------------+

psdf._internal.to_internal_spark_frame.show()
# +-----------------+---+---+---+---+---+
# |__index_level_0__|  A|  B|  C|  D|  E|
# +-----------------+---+---+---+---+---+
# |                0|  1|  5|  9| 13| 17|
# |                1|  2|  6| 10| 14| 18|
# |                2|  3|  7| 11| 15| 19|
# |                3|  4|  8| 12| 16| 20|
# +-----------------+---+---+---+---+---+
```
