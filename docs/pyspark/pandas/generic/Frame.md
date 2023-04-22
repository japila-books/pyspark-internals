# Frame

`Frame` is an [abstraction](#contract) of [frames](#implementations) that behave like [pandas.DataFrame]({{ pandas.api }}/pandas.DataFrame.html) and [pandas.Series]({{ pandas.api }}/pandas.Series.html).

```py
class Frame(object, metaclass=ABCMeta)
```

## Contract

### <span id="__getitem__"> \_\_getitem\_\_ { #__getitem }

```py
@abstractmethod
def __getitem__(
  self,
  key: Any) -> Any
```

```py
class hello():
  def __getitem__(self, key):
    print(f"__getitem__({key})")

h = hello()

>>> h[4]
__getitem__(4)
```

### _internal { #_internal }

```py
@property
@abstractmethod
def _internal(
  self) -> InternalFrame
```

## Implementations

* [DataFrame](../DataFrame.md)
* `Series`
