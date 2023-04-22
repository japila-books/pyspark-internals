# pandas API on Spark

**pandas API on Spark** ([pyspark.pandas](../pyspark/pandas/index.md) package) has been added to PySpark to execute [pandas]({{ pandas.home }}) code on Spark clusters with no changes (except the import).

There are two related PySpark packages with pandas support:

* [pyspark.pandas](../pyspark/pandas/index.md)
* [pyspark.sql.pandas](../pyspark/sql/pandas/index.md)

!!! note "Spark Structured Streaming"
    pandas API on Spark does not support Spark Structured Streaming (_streaming queries_).

## Modules

pandas API on Spark requires that the following modules to be installed:

Module | Version
-------|--------
 [pandas]({{ pandas.home }}) | 1.0.5
 [PyArrow]({{ arrow.docs }}/python/index.html) | 1.0.0

## PYARROW_IGNORE_TIMEZONE { #PYARROW_IGNORE_TIMEZONE }

For PyArrow 2.0.0 and above, pandas API on Spark requires `PYARROW_IGNORE_TIMEZONE` environment variable to be set to `1` (on the driver and executors).

## <span id="_auto_patch_spark"> PYSPARK_PANDAS_USAGE_LOGGER { #PYSPARK_PANDAS_USAGE_LOGGER }

pandas API on Spark uses `PYSPARK_PANDAS_USAGE_LOGGER` (formerly `KOALAS_USAGE_LOGGER`) environment variable for a usage logger.

## Demo

```py
# The following would be required if we used pandas
# import pandas as pd

# but we don't need it anymore 😊

# The only change is supposed to be this extra `pyspark` prefix
# in the name of the package

import pyspark.pandas as pd
```

=== "Python"

    ```py
    pd.read_csv("people.csv")
    ```

```text
   id  name
0   0  zero
1   1   one
2   2   two
```
