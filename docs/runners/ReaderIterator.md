# ReaderIterator

`ReaderIterator` is an [extension](#contract) of the `Iterator` ([Scala]({{ scala.api }}/scala/collection/Iterator.html)) abstraction for [iterators](#implementations) to [read](#read) `OUT` values.

```scala
abstract class ReaderIterator(...)
extends Iterator[OUT]
```

## Contract

### Reading Value { #read }

```scala
read(): OUT
```

See:

* [PythonArrowOutput](PythonArrowOutput.md#newReaderIterator)
* [PythonRunner](PythonRunner.md#newReaderIterator)
* [PythonUDFRunner](PythonUDFRunner.md#newReaderIterator)

Used when:

* `ReaderIterator` is requested to [hasNext](#hasNext)

## Implementations

* [PythonArrowOutput](PythonArrowOutput.md#newReaderIterator)
* [PythonRunner](PythonRunner.md#newReaderIterator)
* [PythonUDFRunner](PythonUDFRunner.md#newReaderIterator)

## handleEndOfDataSection { #handleEndOfDataSection }

```scala
handleEndOfDataSection(): Unit
```

`handleEndOfDataSection`...FIXME

---

`handleEndOfDataSection` is used when:

* `PythonRunner` is requested to [newReaderIterator](PythonRunner.md#newReaderIterator)
* `PythonArrowOutput` is requested to [newReaderIterator](PythonArrowOutput.md#newReaderIterator)
* `PythonUDFRunner` is requested to [newReaderIterator](PythonUDFRunner.md#newReaderIterator)
