# pandas User-Defined Aggregate Functions

**pandas User-Defined Aggregate Functions** (_pandas UDAFs_) are [PythonUDFs](../pandas-udfs/index.md) (with optional [PandasUDFType.GROUPED_AGG](../pyspark/sql/pandas/PandasUDFType.md#GROUPED_AGG) function type) to used as aggregation functions in [GroupedData.agg](../sql/GroupedData.md#agg) operator.

pandas UDAFs are also known as **Group Aggregate pandas UDFs**.

## Limitations

1. There is no partial aggregation with group aggregate UDFs (i.e., a full shuffle is required).
1. All the data of a group will be loaded into memory, so there is a potential OOM risk if data is skewed and certain groups are too large to fit in memory
1. Group aggregate pandas UDFs and built-in aggregation functions cannot be mixed in a single [GroupedData.agg](../sql/GroupedData.md#agg) operator. Otherwise, the following `AnalysisException` is thrown:

    ```text
    [INVALID_PANDAS_UDF_PLACEMENT] The group aggregate pandas UDF `my_udaf` cannot be invoked together with as other, non-pandas aggregate functions.
    ```

## Demo

```py
import pandas as pd
from pyspark.sql.functions import pandas_udf
```

```py
@pandas_udf(returnType = "long")
def my_count(s: pd.Series) -> 'long':
    return pd.Series(s.count())
```

```py
from pyspark.sql.functions import abs
nums = spark.range(5) # FIXME More meaningful dataset
grouped_nums = (nums
    .withColumn("gid", abs((nums.id * 100) % 2))
    .groupBy("gid"))
count_by_gid_agg = my_count("gid").alias("count")
counts_by_gid = grouped_nums.agg(count_by_gid_agg)
```

```py
counts_by_gid.show()
```
