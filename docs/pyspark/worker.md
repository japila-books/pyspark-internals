# worker.py

`worker.py` is a Python module in [pyspark](index.md) package.

```py
from pyspark import worker
```

## <span id="__main__"> Entry Point

??? note "Top-Level Code Environment"
    If the module is executed in the top-level code environment (and not initialized from an import statement), its `__name__` is set to the string `__main__`.

    Sometimes "top-level code" is called an _entry point_ to the application.

    Learn more in the [\_\_main__ — Top-level code environment]({{ python.docs }}/library/__main__.html).

When executed in the top-level code environment (e.g., `python3 -m`), `worker.py` reads the following environment variables:

Environment Variable | Description
---------------------|------------
 `PYTHON_WORKER_FACTORY_PORT` | Port the JVM listens to
 `PYTHON_WORKER_FACTORY_SECRET` | Authorization Secret

`worker.py` [local_connect_and_auth](#local_connect_and_auth) (that gives a `sock_file`).

`worker.py` [write_int](#write_int) with the PID of the Python process to the `sock_file`.

In the end, `worker.py` [main](#main) (with the `sock_file` and `sock_file` for the input and output files).

## main { #main }

```py
main(
    infile,
    outfile)
```

`main` reads `PYTHON_FAULTHANDLER_DIR` environment variable.

`main` does a lot of initializations.

??? note "FIXME Review the initializations"

`main` [read_udfs](#read_udfs) that gives the following:

* `func`
* `profiler`
* `deserializer`
* `serializer`

requests the `deserializer` to `load_stream` from the given `infile` and executes `func` (with the `split_index` and the deserialized stream).

`main` does a lot of post-processings.

??? note "FIXME Review the post-processings"

## read_udfs { #read_udfs }

```py
read_udfs(
    pickleSer,
    infile,
    eval_type)
```

`read_udfs`...FIXME

### read_single_udf { #read_single_udf }

```py
read_single_udf(
    pickleSer,
    infile,
    eval_type,
    runner_conf,
    udf_index)
```

`read_single_udf`...FIXME
