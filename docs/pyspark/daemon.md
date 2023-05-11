# daemon.py

`daemon.py` is a Python module in [pyspark](index.md) package.

```py
from pyspark import daemon
```

## <span id="__main__"> Entry Point

??? note "Top-Level Code Environment"
    If the module is executed in the top-level code environment (e.g., `python -m`), its `__name__` is set to the string `__main__`.

    Sometimes "top-level code" is called an _entry point_ to the application.

    Learn more in the [\_\_main__ — Top-level code environment]({{ python.docs }}/library/__main__.html).

When executed in the top-level code environment, `daemon.py` calls [manager](#manager) function.

## manager { #manager }

```py
manager()
```

`manager` runs until it is stopped (e.g., `CTRL-C`).

`manager` creates a new process group (`os.setpgid(0, 0)`).

`manager` creates a listening socket on the loopback interface (possibly using IPv6 based on `SPARK_PREFER_IPV6` environment variable).

`manager` reads `SPARK_REUSE_WORKER` environment variable (`reuse`).

`manager` launches a [worker process](#worker) (in a child process using `os.fork()`).

### Launching Worker Process { #worker }

```py
worker(
  sock: socket,
  authenticated: Bool) -> Optional[int]
```

!!! note
    `worker` is called by a worker process after the`os.fork()`.

`worker` [runs a worker](worker.md#main).
