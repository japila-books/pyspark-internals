# DataFrame

`DataFrame` is a Python class with [PandasMapOpsMixin](PandasMapOpsMixin.md) and [PandasConversionMixin](PandasConversionMixin.md) mixins.

`DataFrame` is in `pyspark.sql.dataframe` module.

```py
from pyspark.sql.dataframe import DataFrame
```

## Creating Instance

`DataFrame` takes the following to be created:

* <span id="jdf"><span id="_jdf"> jdf
* <span id="sql_ctx"> [SQLContext](SQLContext.md)

## <span id="groupBy"> groupBy

```scala
groupBy(self, *cols)
```

`groupBy` requests the [_jdf](#jdf) to `groupBy` and creates a [GroupedData](GroupedData.md) with it.

## observe { #observe }

```py
observe(
  self,
  observation: Union["Observation", str],
  *exprs: Column,
) -> "DataFrame"
```

`observe` accepts an [Observation](Observation.md) or a name as the `observation`:

* For an [Observation](Observation.md), `observe` requests it to [_on](Observation.md#_on) (with this `DataFrame` and the `exprs` columns).

* For a name, `observe` creates a new `DataFrame` after requesting [_jdf](#_jdf) to `observe` (with the name).

### Demo { #observe-demo }

!!! note "QueryExecutionListener"
    You should install `QueryExecutionListener` ([Spark SQL]({{ book.spark_sql }}/QueryExecutionListener)) to intercept `QueryExecution` on a successful query execution (to access `observedMetrics`).

```py
import pandas as pd

pandas_df = pd.DataFrame({
  'name': ['jacek', 'agata', 'iweta', 'patryk', 'maksym'],
  'age': [50, 49, 29, 26, 11]
  })
df = spark.createDataFrame(pandas_df)
```

```py
from pyspark.sql.functions import *
row_count_metric = count(lit(1)).alias("count")
observed_df = df.observe("observe_demo", row_count_metric)
```

```py
observed_df.count()
```
