# pandas User-Defined Functions

**pandas User-Defined Functions** (_Vectorized User-Defined Functions_ or _pandas UDFs_) are user-defined functions that are executed using Apache Arrow to transfer data and pandas to work with the data, which allows for vectorized operations.

Pandas UDFs are defined using [@pandas_udf](#pandas_udf) decorator (that belongs to [pyspark.sql.functions](../pyspark/sql/functions.md) module).

```py
from pyspark.sql.functions import pandas_udf
```

A Pandas UDF behaves as a regular PySpark function API in general.

As of Spark 3.0 with Python 3.6+, using [Python type hints](https://www.python.org/dev/peps/pep-0484) to specify type hints for the pandas UDF is encouraged (instead of specifying pandas UDF type via `functionType` argument).

The type hint should use `pandas.Series` in most cases (except `pandas.DataFrame`).

**pandas User-Defined Functions** (_pandas UDFs_) are defined using .

## pandas_udf { #pandas_udf }

```py
pandas_udf(
  f=None,
  returnType=None,
  functionType=None)
```

[pandas_udf](../pyspark/sql/pandas/functions.md#pandas_udf) function is used a decorator (using `@pandas_udf` annotation).

## Examples

```py
import pandas as pd
from pyspark.sql.functions import pandas_udf
```

```py
@pandas_udf("string")
def to_upper(s: pd.Series) -> pd.Series:
    return s.str.upper()
```

```py
@pandas_udf("string")
def my_concat(names: pd.Series, ages: pd.Series) -> pd.Series:
    return pd.Series([f"{n} is {a} years old" for (n, a) in zip(names, ages)])
```

```py
pandas_df = pd.DataFrame({
  'name': ['jacek', 'agata', 'iweta', 'patryk', 'maksym'],
  'age': [50, 49, 29, 26, 11]
  })
df = spark.createDataFrame(pandas_df)
```

```text
>>> df.show()
+------+---+
|  name|age|
+------+---+
| jacek| 50|
| agata| 49|
| iweta| 29|
|patryk| 26|
|maksym| 11|
+------+---+
```

```text
>>> df.printSchema()
root
 |-- name: string (nullable = true)
 |-- age: long (nullable = true)
```

```py
df.select(to_upper(df.name).alias("upper_name")).show()
```

```text
+----------+
|upper_name|
+----------+
|     JACEK|
|     AGATA|
|     IWETA|
|    PATRYK|
|    MAKSYM|
+----------+
```

=== "Python"

    ```py
    df.select(my_concat(df.name, df.age)).show(truncate = False)
    ```

```text
+----------------------+
|my_concat(name, age)  |
+----------------------+
|jacek is 50 years old |
|agata is 49 years old |
|iweta is 29 years old |
|patryk is 26 years old|
|maksym is 11 years old|
+----------------------+
```
