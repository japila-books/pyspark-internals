# DataFrame

`DataFrame` is a [Frame](generic/Frame.md) with an [InternalFrame](InternalFrame.md).

`DataFrame` is a `Generic[T]` ([Python]({{ python.api }}/library/typing.html#user-defined-generic-types)).

## Creating Instance

`DataFrame` takes the following to be created:

* <span id="data"> data (optional)
* <span id="index"> index (optional)
* <span id="columns"> columns (optional)
* <span id="dtype"> dtype (optional)
* <span id="copy"> copy (optional)

### _internal_frame { #_internal_frame }

`DataFrame` is given or creates an [InternalFrame](InternalFrame.md) when [created](#creating-instance).

```py
object.__setattr__(self, "_internal_frame", internal)
```

## InternalFrame { #_internal }

??? note "Frame"

    ```py
    @property
    def _internal(
        self) -> InternalFrame
    ```

    `_internal` is part of the [Frame](generic/Frame.md#_internal) abstraction.

`_internal` returns the [_internal_frame](#_internal_frame) (that is expected to be of type [InternalFrame](InternalFrame.md)).
