# spark-submit shell script

`spark-submit` is a command-line application ([Spark Core]({{ book.spark_core }}/tools/spark-submit)) to manage Spark applications, incl. PySpark.

```text
spark-submit 1.py extra args
```

For a PySpark application, `spark-submit` uses [PythonRunner](PythonRunner.md) and launches an extra python process:

```text
ps -o pid,ppid,command | grep python | grep -v grep
```

```text
org.apache.spark.deploy.SparkSubmit 1.py extra args
```

```text
Python /usr/local/bin/ipython 1.py extra args
```
