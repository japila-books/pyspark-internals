# UserDefinedPythonFunction

## Creating Instance

`UserDefinedPythonFunction` takes the following to be created:

* <span id="name"> Name
* <span id="func"> `PythonFunction`
* <span id="dataType"> `DataType` ([Spark SQL]({{ book.spark_sql }}/DataType))
* <span id="pythonEvalType"> Python Eval Type
* <span id="udfDeterministic"> `udfDeterministic` flag

`UserDefinedPythonFunction` is created when:

* `SparkConnectPlanner` ([Spark Connect](../connect/index.md)) is requested to `handleRegisterPythonUDF`
* `UserDefinedFunction` ([pyspark/sql/udf.py](../pyspark/sql/udf.md)) is requested to [_create_judf](../pyspark/sql/UserDefinedFunction.md#_create_judf)

## <span id="builder"> Creating PythonUDF

```scala
builder(
  e: Seq[Expression]): Expression
```

`builder` creates a [PythonUDF](PythonUDF.md) (for all the [arguments](#creating-instance) and the given children expressions).

---

`builder` is used when:

* `UDFRegistration` is requested to register a Python UDF ([Spark SQL]({{ book.spark_sql }}/UDFRegistration#registerPython))
* `UserDefinedPythonFunction` is requested to [apply](#apply)

## <span id="apply"> Applying PythonUDF

```scala
apply(
  exprs: Column*): Column
```

`apply` [creates a PythonUDF](#builder) (for the input `Column` ([Spark SQL]({{ book.spark_sql }}/Column)) expressions) and wraps it up into a `Column`.

---

`apply` is used when:

* `UDFRegistration` is requested to register a Python UDF ([Spark SQL]({{ book.spark_sql }}/UDFRegistration#registerPython))
* `UserDefinedPythonFunction` is requested to [apply](#apply)
