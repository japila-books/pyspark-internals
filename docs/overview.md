# PySpark

**PySpark** is the Python API for Apache Spark.

## shell.py

`pyspark` shell script loads the PySpark `shell.py` script used interactively.

```text
${SPARK_HOME}/python/pyspark/shell.py
```

## pyspark.sql Package

`pyspark.sql` is a Python package for Spark SQL.

```python
from pyspark.sql import *
```

!!! tip
    Learn more about [Modules and Packages](https://docs.python.org/3/tutorial/modules.html) in Python in [The Python Tutorial](https://docs.python.org/3/tutorial/index.html).

### \_\_init\__.py

The `__init__.py` files are required to make Python treat directories containing the file as packages.

Per [6.4.1. Importing * From a Package](https://docs.python.org/3/tutorial/modules.html#importing-from-a-package):

> The import statement uses the following convention: if a package's `__init__.py` code defines a list named `__all__`, it is taken to be the list of module names that should be imported when `from package import *` is encountered.

Per [Public and Internal Interfaces](https://www.python.org/dev/peps/pep-0008/#public-and-internal-interfaces) in [PEP 8 -- Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/):

> To better support introspection, modules should explicitly declare the names in their public API using the `__all__` attribute.

From `python/pyspark/sql/__init__.py`:

```python
__all__ = [
    'SparkSession', 'SQLContext', 'HiveContext', 'UDFRegistration',
    'DataFrame', 'GroupedData', 'Column', 'Catalog', 'Row',
    'DataFrameNaFunctions', 'DataFrameStatFunctions', 'Window', 'WindowSpec',
    'DataFrameReader', 'DataFrameWriter', 'PandasCogroupedOps'
]
```

## pandas

The minimum version of [Pandas](https://pandas.pydata.org/) is `0.23.2` (and [PandasConversionMixin](PandasConversionMixin.md) asserts that).

```python
import pandas as pd
```

## pyarrow

The minimum version of [PyArrow](https://pypi.org/project/pyarrow/) is `1.0.0` (and [PandasConversionMixin](PandasConversionMixin.md) asserts that).

```python
import pyarrow
```

## Python Mixins

From [8.7. Class definitions](https://docs.python.org/3/reference/compound_stmts.html#class-definitions):

> classdef    ::=  [decorators] "class" classname [inheritance] ":" suite
>
> The inheritance list usually gives a list of base classes

PySpark uses mixins:

* [PandasConversionMixin](PandasConversionMixin.md)
* [PandasMapOpsMixin](PandasMapOpsMixin.md)
* [SparkConversionMixin](SparkConversionMixin.md)
