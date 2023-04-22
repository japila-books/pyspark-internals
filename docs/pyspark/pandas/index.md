# pyspark.pandas Package

When imported (that triggers `__init__.py`), `pyspark.pandas` does _monkey-patching_ of `pandas.DataFrame` and `pandas.Series` classes (using [\_\_class_getitem__]({{ python.docs }}/reference/datamodel.html#emulating-generic-types) dunder method).

Pandas | PySpark
-------|--------
[pandas.DataFrame]({{ pandas.api }}/pandas.DataFrame.html) | `pyspark.pandas.frame.DataFrame`
[pandas.Series]({{ pandas.api }}/pandas.Series.html) | `pyspark.pandas.series.Series`
