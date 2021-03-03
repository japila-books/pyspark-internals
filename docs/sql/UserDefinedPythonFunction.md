# UserDefinedPythonFunction

## Creating Instance

`UserDefinedPythonFunction` takes the following to be created:

* <span id="name"> Name
* <span id="func"> `PythonFunction`
* <span id="dataType"> `DataType` ([Spark SQL]({{ book.spark_sql }}/DataType))
* <span id="pythonEvalType"> Python Eval Type
* <span id="udfDeterministic"> `udfDeterministic` flag

## <span id="builder"> Creating PythonUDF

```scala
builder(
  e: Seq[Expression]): Expression
```

`builder` creates a [PythonUDF](PythonUDF.md) for the [arguments](#creating-instance) and the given children expressions.

`builder` is used when:

* `UDFRegistration` is requested to register a Python UDF ([Spark SQL]({{ book.spark_sql }}/UDFRegistration#registerPython))
* `UserDefinedPythonFunction` is requested to [apply](#apply)

## <span id="apply"> Applying PythonUDF

```scala
apply(
  exprs: Column*): Column
```

`apply` [creates a PythonUDF](#builder) with the input `Column` ([Spark SQL]({{ book.spark_sql }}/Column)) expressions and creates a new `Column`.

`apply` is used when:

* `UDFRegistration` is requested to register a Python UDF ([Spark SQL]({{ book.spark_sql }}/UDFRegistration#registerPython))
* `UserDefinedPythonFunction` is requested to [apply](#apply)
