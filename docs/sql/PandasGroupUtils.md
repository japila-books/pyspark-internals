# PandasGroupUtils

## executePython { #executePython }

```scala
executePython[T](
    data: Iterator[T],
    output: Seq[Attribute],
    runner: BasePythonRunner[T, ColumnarBatch]): Iterator[InternalRow]
```

`executePython`...FIXME

---

`executePython` is used when:

* `FlatMapCoGroupsInPandasExec` and [FlatMapGroupsInPandasExec](FlatMapGroupsInPandasExec.md#doExecute) physical operators are executed
