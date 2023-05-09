# Observation

`Observation` is a Python class to observe (named) metrics on a [DataFrame](DataFrame.md).

```py
from pyspark.sql.observation import Observation
```

??? note "pyspark.sql"
    `Observation` is imported using `*` import from `pyspark.sql` as well as `pyspark.sql.observation` (as is included in `__all__` of the modules).

    ```py
    from pyspark.sql import *
    ```

## Creating Instance

`Observation` takes the following to be created:

* <span id="name"><span id="_name"> Name (optional)

## _jo { #_jo }

```py
_jo: Optional[JavaObject]
```

## get { #get }

```py
get(
  self) -> Dict[str, Any]
```

`get` requests the [_jo](#_jo) to `getAsJava` and converts the py4j `JavaMap` to a Python dict.

## Demo

```py
from pyspark.sql.observation import Observation

observation = Observation("demo")
```

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
observed_df = df.observe(observation, row_count_metric)
```

```py
observed_df.count()
```

=== "Python"

    ```py
    observation.get()
    ```

```text
{'count': 5}
```
