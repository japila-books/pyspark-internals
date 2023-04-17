# UDFRegistration

`UDFRegistration` is available as `spark.udf`.

## register { #register }

```python
register(
  self,
  name: str,
  f: Union[Callable[..., Any], "UserDefinedFunctionLike"],
  returnType: Optional[Union[pyspark.sql.types.DataType, str]] = None,
) -> "UserDefinedFunctionLike"
```

`register` registers a Python function (incl. lambda function) or a user-defined function as a SQL function (under the given `name`).

Function `f` | Description
-------------|------------
 A Python function | <ul><li>Includes lambda (_unnamed_) functions<li>`Callable[..., Any]`<li>The return type is `StringType` when not specified<li>Always `PythonEvalType.SQL_BATCHED_UDF`</ul>
 `pyspark.sql.functions.udf` | <ul><li>_row-at-a-time_<li>`UserDefinedFunctionLike`
 `pyspark.sql.functions.pandas_udf` | <ul><li>_vectorized_<li>`UserDefinedFunctionLike`

`evalType` of the a user-defined function can be one of the following:

* `PythonEvalType.SQL_BATCHED_UDF`
* `PythonEvalType.SQL_SCALAR_PANDAS_UDF`
* `PythonEvalType.SQL_SCALAR_PANDAS_ITER_UDF`
* `PythonEvalType.SQL_GROUPED_AGG_PANDAS_UDF`

---

`register` [_create_udf](#_create_udf) and requests the `_jsparkSession` for the `UDFRegistration` ([Spark SQL]({{ book.spark_sql }}/user-defined-functions/UDFRegistration/)) to `registerPython` ([Spark SQL]({{ book.spark_sql }}/user-defined-functions/UDFRegistration/#registerPython)).

```python
from pyspark.sql.functions import call_udf, col
from pyspark.sql.types import IntegerType, StringType

rows = [(1, "a"),(2, "b"), (3, "c")]
columns = ["id", "name"]
df = spark.createDataFrame(rows, columns)

spark.udf.register("intX2", lambda i: i * 2, IntegerType())
df.select(call_udf("intX2", "id")).show()
```
