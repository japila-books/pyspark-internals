# PythonWorkerFactory

## Creating Instance

`PythonWorkerFactory` takes the following to be created:

* <span id="pythonExec"> [Python Executable](PythonFunction.md#pythonExec)
* <span id="envVars"> Environment Variables

`PythonWorkerFactory` is created when:

* `SparkEnv` is requested to `createPythonWorker` (when `BasePythonRunner` is requested to [compute a partition](runners/BasePythonRunner.md#compute)).

## useDaemon { #useDaemon }

`PythonWorkerFactory` initializes `useDaemon` internal flag when [created](#creating-instance).

`useDaemon` is enabled when the following all hold:

* [spark.python.use.daemon](configuration-properties.md#spark.python.use.daemon) is enabled
* The operating system is not MS Windows (based on `os.name` JVM property) as it works on UNIX-based systems only (because it uses signals for child management)

`useDaemon` flag is used when `PythonWorkerFactory` is requested for the following:

* [create](#create)
* [stopDaemon](#stopDaemon)
* [stopWorker](#stopWorker)
* [releaseWorker](#releaseWorker)

## Daemon Process { #daemon }

```scala
daemon: Process = null
```

`daemon` is a `Process` ([Java]({{ java.api }}/java/lang/Process.html)) to control [Python worker processes](#daemonWorkers).

`daemon` is uninitialized (`null`) right after `PythonWorkerFactory` is [created](#creating-instance) and right after [stopDaemon](#stopDaemon).

`daemon` is initialized and immediately started when [startDaemon](#startDaemon) (and listens at [daemonPort](#daemonPort)).

`daemon` is alive until [stopDaemon](#stopDaemon).

Any communication with the `daemon` happens through [daemonPort](#daemonPort).

### Port { #daemonPort }

```scala
daemonPort: Int = 0
```

`daemonPort` is the communication channel (port) of the [daemon](#daemon) Python process (that is known only after [startDaemon](#startDaemon)).

`daemonPort` (alongside the [daemonHost](#daemonHost)) is used to open a socket stream and launch [workers](#daemonWorkers).

### Python Workers { #daemonWorkers }

```scala
daemonWorkers: mutable.WeakHashMap[Socket, Int]
```

`PythonWorkerFactory` creates `daemonWorkers` internal registry of socket streams and the worker's PID when [created](#creating-instance).

A new pair is added in [createSocket](#createSocket) (when [createThroughDaemon](#createThroughDaemon)).

`daemonWorkers` is used when:

* [create](#create) (with [useDaemon](#useDaemon) flag enabled and non-empty [idleWorkers](#idleWorkers))
* [stopWorker](#stopWorker)

## Python Modules

### Daemon { #daemonModule }

`PythonWorkerFactory` initializes `daemonModule` internal property for the **Python Daemon Module** when [created](#creating-instance).

`daemonModule` is the value of [spark.python.daemon.module](configuration-properties.md#spark.python.daemon.module) configuration property (if defined) or `pyspark.daemon`.

The Python Daemon Module is used when `PythonWorkerFactory` is requested to [create and start a daemon module](#startDaemon).

### Worker { #workerModule }

`PythonWorkerFactory` uses [spark.python.worker.module](configuration-properties.md#PYTHON_WORKER_MODULE) configuration property to specify the **Python Worker Module**.

The Python Worker Module is used when `PythonWorkerFactory` is requested to [create and start a worker](#createSimpleWorker).

## Creating Python Worker { #create }

```scala
create(): (Socket, Option[Int])
```

`create` branches off based on [useDaemon](#useDaemon) flag:

* When enabled, `create` firstly checks the [idleWorkers](#idleWorkers) queue and returns one if available. Otherwise, `create` [createThroughDaemon](#createThroughDaemon)
* When disabled, `create` [createSimpleWorker](#createSimpleWorker)

---

`create` is used when:

* `SparkEnv` is requested to `createPythonWorker`

### Creating Daemon Worker { #createThroughDaemon }

```scala
createThroughDaemon(): (Socket, Option[Int])
```

`createThroughDaemon` [startDaemon](#startDaemon) followed by [createSocket](#createSocket).

In case of a `SocketException`, `createThroughDaemon` prints out the following WARN message to the logs:

```text
Failed to open socket to Python daemon: [exception]
Assuming that daemon unexpectedly quit, attempting to restart
```

And then, `createThroughDaemon` [stopDaemon](#stopDaemon), [startDaemon](#startDaemon) and [createSocket](#createSocket).

#### createSocket { #createSocket }

```scala
createSocket(): (Socket, Option[Int])
```

`createSocket` creates a new stream socket and connects it to the [daemonPort](#daemonPort) at the [daemonHost](#daemonHost).

`createSocket` reads the PID (of the python worker behind the stream socket) and requests the [authHelper](#authHelper) to `authToServer`.

In the end, `createSocket` returns the socket and the PID (after registering them in the [daemonWorkers](#daemonWorkers) registry).

### Starting Python Daemon Process { #startDaemon }

```scala
startDaemon(): Unit
```

!!! note "Does nothing with `daemon` initialized"
    `startDaemon` does nothing when [daemon](#daemon) is initialized (non-`null`) that indicates that the daemon is already up and running.

`startDaemon` creates the command (using the given [pythonExec](#pythonExec) and the [daemon module](#daemonModule)):

```text
[pythonExec] -m [daemonModule]
```

`startDaemon` adds the given [envVars](#envVars) and the following (extra) environment variables to the environment of future python processes:

Environment Variable | Value
---------------------|------
 `PYTHONPATH` | [pythonPath](#pythonPath)
 `PYTHON_WORKER_FACTORY_SECRET` | [authHelper](#authHelper)
 `SPARK_PREFER_IPV6` | `True` if the underlying JVM prefer IPv6 addresses (based on `java.net.preferIPv6Addresses` JVM property)
 `PYTHONUNBUFFERED` | `YES`

`startDaemon` starts a new process (that is known as the [daemon](#daemon)).

`startDaemon` connects to the python process to read the [daemonPort](#daemonPort).

In the end, `startDaemon` [redirectStreamsToStderr](#redirectStreamsToStderr).

## <span id="createSimpleWorker"> Creating Simple Non-Daemon Worker

```scala
createSimpleWorker(): Socket
```

`createSimpleWorker`...FIXME

`createSimpleWorker` is used when `PythonWorkerFactory` is requested to [create a Python worker](#create) (with [useDaemon](#useDaemon) flag disabled).

## Logging

Enable `ALL` logging level for `org.apache.spark.api.python.PythonWorkerFactory` logger to see what happens inside.

Add the following line to `conf/log4j2.properties`:

```text
logger.PythonWorkerFactory.name = org.apache.spark.api.python.PythonWorkerFactory
logger.PythonWorkerFactory.level = all
```

Refer to [Logging](logging.md).
