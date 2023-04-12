---
status: new
---

# TorchDistributor

`TorchDistributor` is a [Distributor](Distributor.md).

```py
from pyspark.ml.torch.distributor import TorchDistributor

distributor = TorchDistributor(
    num_processes=1,
    local_mode=True,
    use_gpu=False)

# accepts a Callable (function) or a path to a training script
# and variable-length kwargs
distributor.run(
    "train.py",    # a training script
    "--learning-rate=1e-3",
    "--batch-size=64",
    "--my-key=my-value")

# Started local training with 1 processes
# NOTE: Redirects are currently not supported in Windows or MacOs.
# Finished local training with 1 processes
```

## Running Distributed Training { #run }

```py
run(
    self,
    train_object: Union[Callable, str],
    *args: Any) -> Optional[Any]
```

`run`...FIXME
