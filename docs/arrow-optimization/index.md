# Arrow Optimization

**Arrow Optimization** is an optimization that uses [Apache Arrow]({{ arrow.home }}) for columnar data transfers in the following:

* [pyspark.sql.DataFrame.toPandas](../sql/PandasConversionMixin.md#toPandas)
* [pyspark.sql.SparkSession.createDataFrame](../sql/SparkConversionMixin.md#createDataFrame) (when called with a Pandas `DataFrame` or a NumPy `ndarray`)

The following data types are unsupported: `ArrayType` of `TimestampType`.
