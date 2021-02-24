# Building from Sources

```text
./build/mvn \
  -Pyarn,kubernetes,hive,hive-thriftserver,scala-2.12 \
  -DskipTests \
  clean install
```

## Building PySpark-Related Operators

```text
./build/mvn -DskipTests -pl :spark-sql_2.12 clean install
```

```text
cp sql/core/target/spark-sql_2.12-3.1.1.jar assembly/target/scala-2.12/jars/
```
