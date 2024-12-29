# User-Defined Table Functions (UDTFs)

**User-Defined Table Functions (UDTFs)** are user-defined functions that...FIXME

```py
from pyspark.sql.functions import udtf
from pyspark.sql import Row

udtf(returnType="a: int")
class TestUDTF:
    def eval(self, row: Row):
        if row[0] > 5:
            yield row[0]
    
    def terminate(self):
        """
        This method is optional, but
        there's a bug in 3.5.4 that makes terminate required
        https://issues.apache.org/jira/browse/SPARK-50674
        """
        pass
```

```py
spark.udtf.register("test_udtf", TestUDTF)
```

```py
spark.sql("SELECT * FROM test_udtf(range(0, 8)) PARTITION BY id)").show()
```
