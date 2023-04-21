# Spark Connect

PySpark supports remote connection to Spark clusters using Spark Connect ([Spark SQL]({{ book.spark_sql }}/connect)).

```console
$ ./bin/pyspark --help
Usage: ./bin/pyspark [options]

Options:
 Spark Connect only:
   --remote CONNECT_URL       URL to connect to the server for Spark Connect, e.g.,
                              sc://host:port. --master and --deploy-mode cannot be set
                              together with this option. This option is experimental, and
                              might change between minor releases.
 ...
```

Spark Connect for Python requires the following Python libraries:

Module | Version
-------|--------
[pandas](https://pandas.pydata.org/) | 1.0.5
[pyarrow](https://arrow.apache.org/docs/python/index.html) | 1.0.0
[grpc](https://grpc.io/docs/languages/python/) | 1.48.1

```console
// switching to an conda environment with the libraries
$ conda activate pyspark

$ ./bin/pyspark --remote sc://localhost
Python 3.10.10 (main, Mar 21 2023, 13:41:39) [Clang 14.0.6 ] on darwin
Type "help", "copyright", "credits" or "license" for more information.
Welcome to
      ____              __
     / __/__  ___ _____/ /__
    _\ \/ _ \/ _ `/ __/  '_/
   /__ / .__/\_,_/_/ /_/\_\   version 3.4.0
      /_/

Using Python version 3.10.10 (main, Mar 21 2023 13:41:39)
Client connected to the Spark Connect server at localhost
SparkSession available as 'spark'.

>>> spark.client
<pyspark.sql.connect.client.SparkConnectClient object at 0x7fed8867ab90>
```

## is_remote { #is_remote }

```py
# from pyspark.sql.utils import is_remote
is_remote() -> bool
```

`is_remote` is `True` when `SPARK_REMOTE` environment variable is defined (in `os.environ`).
