# PythonRDD

`PythonRDD` is an `RDD` (`RDD[Array[Byte]]`) that uses [PythonRunner](PythonRunner.md) (to [compute a partition](#compute)).

## Creating Instance

`PythonRDD` takes the following to be created:

* <span id="parent"> Parent `RDD`
* <span id="func"> [PythonFunction](PythonFunction.md)
* <span id="preservePartitoning"> `preservePartitoning` flag
* <span id="isFromBarrier"> `isFromBarrier` flag (default: `false`)

`PythonRDD` is created when...FIXME

## <span id="runJob"> runJob

```scala
runJob(
  sc: SparkContext,
  rdd: JavaRDD[Array[Byte]],
  partitions: JArrayList[Int]): Array[Any]
```

`runJob`...FIXME

## <span id="collectAndServe"> collectAndServe

```scala
collectAndServe[T](
  rdd: RDD[T]): Array[Any]
```

`collectAndServe`...FIXME

## <span id="collectAndServeWithJobGroup"> collectAndServeWithJobGroup

```scala
collectAndServeWithJobGroup[T](
  rdd: RDD[T],
  groupId: String,
  description: String,
  interruptOnCancel: Boolean): Array[Any]
```

`collectAndServeWithJobGroup`...FIXME

## <span id="serveIterator"> serveIterator Utility

```scala
serveIterator(
  items: Iterator[_],
  threadName: String): Array[Any]
```

`serveIterator` [serveToStream](#serveToStream) with a writer function that...FIXME

`serveIterator` is used when:

* `PythonRDD` utility is used to [runJob](#runJob), [collectAndServe](#collectAndServe) and [collectAndServeWithJobGroup](#collectAndServeWithJobGroup)
* `Dataset` is requested to `collectToPython`, `tailToPython`, `getRowsToPython`

## <span id="serveToStream"> serveToStream Utility

```scala
serveToStream(
  threadName: String)(
  writeFunc: OutputStream => Unit): Array[Any]
```

`serveToStream` [serveToStream](SocketAuthServer.md#serveToStream) with the [authHelper](#authHelper) and the input arguments.

`serveToStream` is used when:

* `PythonRDD` utility is used to [serveIterator](#serveIterator)
* `Dataset` is requested to `collectAsArrowToPython`

## <span id="authHelper"> SocketAuthHelper

`PythonRDD` uses a [SocketAuthHelper](SocketAuthHelper.md).
