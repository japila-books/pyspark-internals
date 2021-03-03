# Py4JServer

`Py4JServer` is a gateway server between Python and Java Virtual Machine (JVM) using [Py4J]({{ py4j.doc }}).

`Py4JServer` is a wrapper for a [py4j Server](#server).

## Creating Instance

`Py4JServer` takes the following to be created:

* <span id="sparkConf"> `SparkConf` ([Spark Core]({{ book.spark_core }}/SparkConf))

`Py4JServer` is created when:

* [PythonGatewayServer](PythonGatewayServer.md) command-line application is started
* [PythonRunner](PythonRunner.md) command-line application is started

## <span id="server"> py4j Server

`Py4JServer` creates a `ClientServer` ([py4j]({{ py4j.javadoc }}/py4j/ClientServer.html)) or `GatewayServer` ([py4j]({{ py4j.javadoc }}/py4j/GatewayServer.html)) based on [PYSPARK_PIN_THREAD](environment-variables.md#PYSPARK_PIN_THREAD) environment variable.

## <span id="secret"> Connection Secret

```scala
secret: String
```

`Py4JServer` creates a connection secret for a secure communication.

## <span id="start"> start

```scala
start(): Unit
```

`start` requests the [py4j Server](#server) to start.

## <span id="getListeningPort"> getListeningPort

```scala
getListeningPort: Int
```

`getListeningPort` requests the [py4j Server](#server) for the listening port.
