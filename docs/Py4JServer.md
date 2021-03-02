# Py4JServer

`Py4JServer` is a gateway server.

## <span id="secret"> Connection Secret

```scala
secret: String
```

`Py4JServer` creates a connection secret to establish a secured communication to...FIXME

## <span id="start"> start

```scala
start(): Unit
```

`start`...FIXME

`start` is used when:

* `PythonGatewayServer` is [launched](PythonGatewayServer.md#main)
* `PythonRunner` is [launched](runners/PythonRunner.md#main)

## <span id="getListeningPort"> getListeningPort

```scala
getListeningPort: Int
```

`getListeningPort`...FIXME

`getListeningPort` is used when:

* `PythonGatewayServer` is [launched](PythonGatewayServer.md#main)
* `PythonRunner` is [launched](runners/PythonRunner.md#main)
