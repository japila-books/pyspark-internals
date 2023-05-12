# pandas User-Defined Functions

**pandas User-Defined Functions** (_Vectorized User-Defined Functions_ or _pandas UDFs_) are user-defined functions that are executed using Apache Arrow to transfer data and pandas to work with the data, which allows for vectorized operations.

Pandas UDFs are defined using [@pandas_udf](#pandas_udf) decorator.

A Pandas UDF behaves as a regular PySpark function API in general.

As of Spark 3.0.0 ([SPARK-28264](https://issues.apache.org/jira/browse/SPARK-28264)), using [Python type hints](https://www.python.org/dev/peps/pep-0484) in pandas UDF is encouraged (instead of specifying pandas UDF type via [functionType](#functionType) argument).

The return type (type hint) of a user-defined function should be as follows:

* `pandas.Series` ([pandas]({{ pandas.api }}/pandas.Series.html)) in most cases
* `pandas.DataFrame` ([pandas]({{ pandas.api }}/pandas.DataFrame.html)) for `struct` input or output

## @pandas_udf Decorator { #pandas_udf }

```py
pandas_udf(
  f=None,
  returnType=None,
  functionType=None)
```

[pandas_udf](../pyspark/sql/pandas/functions.md#pandas_udf) function is used a decorator (using `@pandas_udf` annotation).

??? note "Python Decorators"
    Learn more in [PEP 318 – Decorators for Functions and Methods]({{ python.peps }}/pep-0318/).

`pandas_udf` belongs to [pyspark.sql.functions](../pyspark/sql/functions.md) module.

```py
from pyspark.sql.functions import pandas_udf
```

### functionType { #functionType }

`functionType` can be one of [PandasUDFType](../pyspark/sql/pandas/PandasUDFType.md)s (but is currently discouraged in favour of type hints).

```py
@pandas_udf(returnType = "long", functionType = PandasUDFType.GROUPED_AGG)
def my_udaf(names: pd.Series) -> 'long':
  return pd.Series(names.count())
```

`functionType` is also known as `evalType`.

[SQL_SCALAR_PANDAS_UDF](../sql/PythonEvalType.md#SQL_SCALAR_PANDAS_UDF) is the default scalar UDF type.

### returnType { #returnType }

`@pandas_udf` decorator can optionally specify a return type (as the first positional argument or using `returnType`).

A return type can be one of the names of `pyspark.sql.types.DataType` instances or the `DataType` themselves.

```py
@pandas_udf(dataType)
@pandas_udf(returnType=dataType)
```

## pandas UDAFs

[pandas User-Defined Aggregate Functions](../pandas-udafs/index.md).

## Demo

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
(df
  .select(to_upper(df.name).alias("upper_name"))
  .show())
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
