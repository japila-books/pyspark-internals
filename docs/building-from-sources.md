# Building from Sources

```text
$ java -version
openjdk version "11.0.10" 2021-01-19
OpenJDK Runtime Environment AdoptOpenJDK (build 11.0.10+9)
OpenJDK 64-Bit Server VM AdoptOpenJDK (build 11.0.10+9, mixed mode)
```

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
