# Distributor

`Distributor` is the parent (_abstract_) class of [TorchDistributor](TorchDistributor.md).

## Creating Instance

`Distributor` takes the following to be created:

* <span id="num_processes"> Number of processes (default: `1`)
* <span id="local_mode"> `local_mode` flag (default: `True`)
* <span id="use_gpu"> `use_gpu` flag (default: `True`)

!!! note "Abstract Class"
    `Distributor` is not supposed to be created directly.

## _get_num_tasks { #_get_num_tasks }

```py
_get_num_tasks(
  self) -> int
```

`_get_num_tasks`...FIXME

## get_gpus_owned { #get_gpus_owned }

```py
get_gpus_owned(
  context: Union[SparkContext, BarrierTaskContext]) -> List[str]
```

`get_gpus_owned`...FIXME

---

`get_gpus_owned` is used when:

* `TorchDistributor` is requested to [_run_local_training](TorchDistributor.md#_run_local_training) and [_get_spark_task_function](TorchDistributor.md#_get_spark_task_function)
