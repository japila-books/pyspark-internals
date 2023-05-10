# daemon.py

## <span id="__main__"> Entry Point

??? note "Top-Level Code Environment"
    If the module is executed in the top-level code environment (and not initialized from an import statement), its `__name__` is set to the string `__main__`.

    Sometimes "top-level code" is called an _entry point_ to the application.

    Learn more in the [\_\_main__ — Top-level code environment]({{ python.docs }}/library/__main__.html).

When executed in the top-level code environment (e.g., `python3 -m`), `daemon.py` calls [manager](#manager).

## manager { #manager }

```py
manager()
```

`manager`...FIXME

### worker { #worker }

```py
worker(
    sock,
    authenticated)
```

`worker`...FIXME
