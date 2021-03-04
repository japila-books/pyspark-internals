# Demo: Executing PySpark Applications Using spark-submit

PySpark applications are executed using `spark-submit` ([Spark Core]({{ book.spark_core }}/tools/spark-submit)) command-line application.

```text
spark-submit 1.py extra args
```

For a PySpark application, `spark-submit` uses [PythonRunner](../PythonRunner.md) and launches an extra python process:

```text
ps -o pid,ppid,command | grep python | grep -v grep
```

```text
org.apache.spark.deploy.SparkSubmit 1.py extra args
```

```text
Python /usr/local/bin/ipython 1.py extra args
```

## SPARK_PRINT_LAUNCH_COMMAND Environment Variable

Use `SPARK_PRINT_LAUNCH_COMMAND` environment variable to have the complete Spark command printed out to the standard output (cf. [spark-submit shell script]({{ book.spark_core }}/tools/spark-submit/#spark_print_launch_command)).

```text
SPARK_PRINT_LAUNCH_COMMAND=1 spark-submit 1.py extra args
```

## verbose Option

Use `--verbose` option for verbose debugging output.

```text
Parsed arguments:
  ...
  pyFiles                 null
  ...
  primaryResource         file:/Users/jacek/dev/sandbox/python-sandbox/1.py
  name                    1.py
  childArgs               [extra args]
...
Main class:
org.apache.spark.deploy.PythonRunner
Arguments:
file:/Users/jacek/dev/sandbox/python-sandbox/1.py
null
extra
args
Spark config:
(spark.app.name,1.py)
(spark.master,local[*])
(spark.submit.pyFiles,)
(spark.submit.deployMode,client)
```
