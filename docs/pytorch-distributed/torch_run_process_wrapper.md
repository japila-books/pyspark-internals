---
title: torch_run_process_wrapper
---

# torch_run_process_wrapper Module

`torch_run_process_wrapper` is used as the [torchrun command](TorchDistributor.md#_create_torchrun_command) in [TorchDistributor](TorchDistributor.md).

`torch_run_process_wrapper` executes `torch.distributed.run` module (using `python -m`). `torch_run_process_wrapper` monitors the child process and prints out the output to the standard output.
