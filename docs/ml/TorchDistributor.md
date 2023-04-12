---
status: new
---

# TorchDistributor

`TorchDistributor` is a [Distributor](Distributor.md).

```py
from pyspark.ml.torch.distributor import TorchDistributor

distributor = TorchDistributor(
    num_processes=1,
    local_mode=False,
    use_gpu=False)
```

```py
# Use a path to a training script
# and variable-length kwargs
distributor.run(
    "train.py",
    "--learning-rate=1e-3",
    "--batch-size=64",
    "--my-key=my-value")

# Started local training with 1 processes
# NOTE: Redirects are currently not supported in Windows or MacOs.
# Finished local training with 1 processes
```

```py
# Use a Callable (function)
# The number of positional arguments is the number of kwargs
def train(a, b, c):
    print(f"Got a={a}, b={b}, c={c}")
    return 'success'

distributor.run(
    train,
    "--learning-rate=1e-3",
    "--batch-size=64",
    "--my-key=my-value")

# Started distributed training with 1 executor proceses
# NOTE: Redirects are currently not supported in Windows or MacOs.    (0 + 1) / 1]
# NOTE: Redirects are currently not supported in Windows or MacOs.
# Got a=--learning-rate=1e-3, b=--batch-size=64, c=--my-key=my-value
# Got a=--learning-rate=1e-3, b=--batch-size=64, c=--my-key=my-value
# Finished distributed training with 1 executor proceses
# 'success'
```

## Running Distributed Training { #run }

```py
run(
    self,
    train_object: Union[Callable, str],
    *args: Any) -> Optional[Any]
```

`run` determines whether to run a PyTorch function or a script (based on the given `train_object`). For a script, `run` uses [_run_training_on_pytorch_file](#_run_training_on_pytorch_file). Otherwise, `run` uses [_run_training_on_pytorch_function](#_run_training_on_pytorch_function).

In the end, `run` runs the training. In [local mode](Distributor.md#local_mode), `run` [runs local training](#_run_local_training). Otherwise, `run` [runs distributed training](#_run_distributed_training).

### Local Training { #_run_local_training }

```py
_run_local_training(
    self,
    framework_wrapper_fn: Callable,
    train_object: Union[Callable, str],
    *args: Any,
) -> Optional[Any]
```

`_run_local_training` looks up `CUDA_VISIBLE_DEVICES` among the environment variables.

With [use_gpu](Distributor.md#use_gpu), `_run_local_training`...FIXME

`_run_local_training` prints out the following INFO message to the logs:

```text
Started local training with [num_processes] processes
```

`_run_local_training` executes the given `framework_wrapper_fn` function (with the [input_params](#input_params), the given `train_object` and the `args`).

In the end, `_run_local_training` prints out the following INFO message to the logs:

```text
Finished local training with [num_processes] processes
```

### Distributed Training { #_run_distributed_training }

```py
_run_distributed_training(
    self,
    framework_wrapper_fn: Callable,
    train_object: Union[Callable, str],
    *args: Any,
) -> Optional[Any]
```

`_run_distributed_training`...FIXME
