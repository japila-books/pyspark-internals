# DataFrame

`DataFrame` is a Python class with [PandasMapOpsMixin](PandasMapOpsMixin.md) and [PandasConversionMixin](PandasConversionMixin.md) mixins.

`DataFrame` lives in `pyspark.sql.dataframe` module (together with `DataFrameNaFunctions` and `DataFrameStatFunctions`).

```python
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
