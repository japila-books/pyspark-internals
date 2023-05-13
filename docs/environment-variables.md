# Environment Variables

PySpark uses environment variables to configure execution environment.

## PYSPARK_DRIVER_PYTHON { #PYSPARK_DRIVER_PYTHON }

The Python Executable in [PySpark Connect](connect/index.md) when [PYSPARK_PYTHON](#PYSPARK_PYTHON) is not defined

Default: `python3`

## PYSPARK_GATEWAY_PORT { #PYSPARK_GATEWAY_PORT }

## PYSPARK_GATEWAY_SECRET { #PYSPARK_GATEWAY_SECRET }

## PYSPARK_PIN_THREAD { #PYSPARK_PIN_THREAD }

Enables **pinned thread mode** to synchronize PVM threads with JVM threads based on Py4J's [ClientServer]({{ py4j.javadoc }}/py4j/ClientServer.html) (`true`) or [GatewayServer]({{ py4j.javadoc }}/py4j/GatewayServer.html) (`false`)

Default: `false`

Used when:

* [launch_gateway](pyspark/java_gateway.md) is executed
* [Py4JServer](Py4JServer.md) is created (and initializes the [server](Py4JServer.md#server))

## PYSPARK_PYTHON { #PYSPARK_PYTHON }

The Python Executable

Default: `python3`
