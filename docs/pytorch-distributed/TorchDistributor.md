# TorchDistributor

`TorchDistributor` is a [Distributor](../ml/Distributor.md) to run PyTorch's [torch.distributed.run]({{ pytorch.github }}/blob/main/torch/distributed/run.py) module on Apache Spark clusters.

`TorchDistributor` is a PySpark translation of [torchrun]({{ pytorch.docs }}/elastic/run.html) (from [Torch Distributed Elastic]({{ pytorch.docs }}/distributed.elastic.html)).

## Demo

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

`run` determines what to run (e.g., a function or a script based on the given `train_object`).

* With a function, `run` uses [_run_training_on_pytorch_function](#_run_training_on_pytorch_function)
* With a script, `run` uses [_run_training_on_pytorch_file](#_run_training_on_pytorch_file)

In the end, `run` runs a local or distributed training.

* In [local mode](../ml/Distributor.md#local_mode), `run` [runs local training](#_run_local_training)
* In non-[local mode](../ml/Distributor.md#local_mode), `run` [runs distributed training](#_run_distributed_training)

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

With [use_gpu](../ml/Distributor.md#use_gpu), `_run_local_training`...FIXME

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

### _run_training_on_pytorch_function { #_run_training_on_pytorch_function }

```py
_run_training_on_pytorch_function(
    input_params: Dict[str, Any],
    train_fn: Callable,
    *args: Any
) -> Any
```

`_run_training_on_pytorch_function` [prepares train and output files](#_setup_files).

`_run_training_on_pytorch_function`...FIXME

### Setting Up Files { #_setup_files }

```py
# @contextmanager
_setup_files(
    train_fn: Callable,
    *args: Any
) -> Generator[Tuple[str, str], None, None]
```

`_setup_files` gives the paths of a TorchRun train file and `output.pickle` output file.

---

`_setup_files` [creates a save directory](#_create_save_dir).

`_setup_files` [saves train_fn function](#_save_pickled_function) to the save directory (that gives a `pickle_file_path`).

`_setup_files` uses the save directory and `output.pickle` name for the output file path.

`_setup_files` [creates a torchrun_train_file](#_create_torchrun_train_file) with the following:

* [Save directory](#_create_save_dir)
* `pickle_file_path`
* `output.pickle` output file path

In the end, `_setup_files` yields (_gives_) the `torchrun_train_file` and the `output.pickle` output file path.

### Creating TorchRun Train File { #_create_torchrun_train_file }

```py
_create_torchrun_train_file(
    save_dir_path: str,
    pickle_file_path: str,
    output_file_path: str
) -> str
```

`_create_torchrun_train_file` creates `train.py` in the given `save_dir_path` with the following content (based on the given `pickle_file_path` and the `output_file_path`):

```py
import cloudpickle
import os

if __name__ == "__main__":
    with open("[pickle_file_path]", "rb") as f:
        train_fn, args = cloudpickle.load(f)
    output = train_fn(*args)
    with open("[output_file_path]", "wb") as f:
        cloudpickle.dump(output, f)
```

## _run_training_on_pytorch_file { #_run_training_on_pytorch_file }

```py
_run_training_on_pytorch_file(
    input_params: Dict[str, Any],
    train_path: str,
    *args: Any
) -> None
```

`_run_training_on_pytorch_file` looks up the `log_streaming_client` in the given `input_params` (or assumes `None`).

!!! note "FIXME What's log_streaming_client?"

`_run_training_on_pytorch_file` [creates torchrun command](#_create_torchrun_command).

`_run_training_on_pytorch_file` [executes the command](#_execute_command).

### _create_torchrun_command { #_create_torchrun_command }

```py
_create_torchrun_command(
    input_params: Dict[str, Any],
    path_to_train_file: str,
    *args: Any
) -> List[str]
```

`_create_torchrun_command` takes the value of the following parameters (from the given `input_params`):

* `local_mode`
* `num_processes`

`_create_torchrun_command` determines the `torchrun_args` and `processes_per_node` based on `local_mode`.

 local_mode | torchrun_args | processes_per_node
-------------|-----------------|---------------------
`True` | <ul><li>`--standalone`<li>`--nnodes=1`</ul> | `num_processes`<br>(from the given `input_params`)
`False` | <ul><li>`--nnodes=[num_processes]`<li>`--node_rank=[node_rank]`<li>`--rdzv_endpoint=[MASTER_ADDR]:[MASTER_PORT]`<li>`--rdzv_id=0`</ul> | 1

In the end, `_create_torchrun_command` returns a Python command to execute [torch_run_process_wrapper](torch_run_process_wrapper.md) module (`python -m`) with the following positional arguments:

* `torchrun_args`
* `--nproc_per_node=[processes_per_node]`
* The given `path_to_train_file`
* The given `args`
