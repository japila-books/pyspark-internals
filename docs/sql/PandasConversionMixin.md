# PandasConversionMixin

`PandasConversionMixin` is a Python mixin of [DataFrame](DataFrame.md) to [convert to Pandas](#toPandas) ([pandas.DataFrame]({{ pandas.api }}/pandas.DataFrame.html)).

## toPandas { #toPandas }

```python
toPandas(self)
```

`toPandas` can only be used with [DataFrame](DataFrame.md).

With [Arrow optimization](../configuration-properties/index.md#arrowPySparkEnabled) enabled, `toPandas` [to_arrow_schema](#to_arrow_schema).

!!! note "pyarrow"
    Arrow Optimization uses `pyarrow` module.

`toPandas` renames the columns to be of `col_[index]` format and [_collect_as_arrow](#_collect_as_arrow) (with `split_batches` based on `arrowPySparkSelfDestructEnabled` configuration property).

`toPandas` creates a `pyarrow.Table` (from the `RecordBatch`es) and converts the table to a pandas-compatible NumPy array or `DataFrame`. `toPandas` renames the columns back to the initial column names.

!!! note
    Column order is assumed.

With [Arrow optimization](../configuration-properties/index.md#arrowPySparkEnabled) disabled, `toPandas` collects the records (`DataFrame.collect`) and creates a `pandas.DataFrame` (with some type _munging_).
