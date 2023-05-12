# PandasGroupUtils

`PandasGroupUtils` utility is used by the following physical operators when executed:

* `FlatMapCoGroupsInPandasExec`
* [FlatMapGroupsInPandasExec](FlatMapGroupsInPandasExec.md#doExecute)

## executePython { #executePython }

```scala
executePython[T](
  data: Iterator[T],
  output: Seq[Attribute],
  runner: BasePythonRunner[T, ColumnarBatch]): Iterator[InternalRow]
```

`executePython` requests the given [BasePythonRunner](../runners/BasePythonRunner.md) to [compute](../runners/BasePythonRunner.md#compute) the (partition) `data` (with the current task's `TaskContext` and the partition ID).

`executePython`...FIXME

---

`executePython` is used when:

* `FlatMapCoGroupsInPandasExec` and [FlatMapGroupsInPandasExec](FlatMapGroupsInPandasExec.md#doExecute) physical operators are executed

## groupAndProject { #groupAndProject }

```scala
groupAndProject(
  input: Iterator[InternalRow],
  groupingAttributes: Seq[Attribute],
  inputSchema: Seq[Attribute],
  dedupSchema: Seq[Attribute]): Iterator[(InternalRow, Iterator[InternalRow])]
```

`groupAndProject` creates a `GroupedIterator` for the `input` iterator (of `InternalRow`s), the `groupingAttributes` and the `inputSchema`.

`groupAndProject`...FIXME

---

`groupAndProject` is used when:

* `FlatMapCoGroupsInPandasExec` and [FlatMapGroupsInPandasExec](FlatMapGroupsInPandasExec.md#doExecute) physical operators are executed
