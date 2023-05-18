# SparkSession.Builder

## Creating Instance

`Builder` takes no arguments to be created.

`Builder` is created when:

* `SparkSession` is requested for [one](SparkSession.md#builder)

## getOrCreate { #getOrCreate }

```py
getOrCreate(
  self) -> "SparkSession"
```

With `SPARK_REMOTE` environment variable or `spark.remote` configuration property defined, `getOrCreate`...FIXME

`getOrCreate` [_instantiatedSession](SparkSession.md#_instantiatedSession).

Unless `SparkSession` is already created, `getOrCreate` creates [one](SparkSession.md).
