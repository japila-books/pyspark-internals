---
title: EvalPythonExec
---

# EvalPythonExec Unary Physical Operators

`EvalPythonExec` is an [extension](#contract) of the `UnaryExecNode` ([Spark SQL]({{ book.spark_sql }}/physical-operators/UnaryExecNode)) abstraction for [unary physical operators](#implementations) that [evaluate PythonUDFs](#evaluate) (when [executed](#doExecute)).

## Contract

### Evaluating PythonUDFs { #evaluate }

```scala
evaluate(
  funcs: Seq[ChainedPythonFunctions],
  argOffsets: Array[Array[Int]],
  iter: Iterator[InternalRow],
  schema: StructType,
  context: TaskContext): Iterator[InternalRow]
```

See:

* [ArrowEvalPythonExec](ArrowEvalPythonExec.md#evaluate)

Used when:

* `EvalPythonExec` physical operator is requested to [doExecute](#doExecute)

### Result Attributes { #resultAttrs }

```scala
resultAttrs: Seq[Attribute]
```

Result `Attribute`s ([Spark SQL]({{ book.spark_sql }}/expressions/Attribute))

See:

* [ArrowEvalPythonExec](ArrowEvalPythonExec.md#resultAttrs)

Used when:

* `EvalPythonExec` physical operator is requested for the [output](#output) and [producedAttributes](#producedAttributes)

### Python UDFs { #udfs }

```scala
udfs: Seq[PythonUDF]
```

[PythonUDF](PythonUDF.md)s to [evaluate](#evaluate)

See:

* [ArrowEvalPythonExec](ArrowEvalPythonExec.md#udfs)

Used when:

* `EvalPythonExec` physical operator is requested to [doExecute](#doExecute)

## Implementations

* [ArrowEvalPythonExec](ArrowEvalPythonExec.md)
* `BatchEvalPythonExec`

## Executing Physical Operator { #doExecute }

??? note "SparkPlan"

    ```scala
    doExecute(): RDD[InternalRow]
    ```

    `doExecute` is part of the `SparkPlan` ([Spark SQL]({{ book.spark_sql }}/physical-operators/SparkPlan#doExecute)) abstraction.

The gist of `doExecute` is to [evaluate Python UDFs](#evaluate) (for every `InternalRow`) with some pre- and post-processing.

---

`doExecute` requests the child physical operator to `execute` (to produce an input `RDD[InternalRow]`).

!!! note
    `EvalPythonExec`s are `UnaryExecNode`s ([Spark SQL]({{ book.spark_sql }}/physical-operators/UnaryExecNode)).

`doExecute` uses `RDD.mapPartitions` operator to execute a function over partitions of `InternalRow`s.

For every partition, `doExecute` creates a `MutableProjection` for the inputs (and the child's output) and requests it to `initialize`.

`doExecute` [evaluates Python UDFs](#evaluate) (for every `InternalRow`).

In the end, `doExecute` creates an `UnsafeProjection` for the [output](#output) to "map over" the rows (from evaluating Python UDFs).
