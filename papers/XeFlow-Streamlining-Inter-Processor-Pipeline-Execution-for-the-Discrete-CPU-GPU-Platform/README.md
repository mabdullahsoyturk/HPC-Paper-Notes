# XeFlow: Streamlining Inter-Processor Pipeline Execution for the Discrete CPU-GPU Platform

Z. Li, B. Peng and C. Weng, "XeFlow: Streamlining Inter-Processor Pipeline Execution for the Discrete CPU-GPU Platform," in IEEE Transactions on Computers, vol. 69, no. 6, pp. 819-831, 1 June 2020, doi: 10.1109/TC.2020.2968302.

## What
They provide a new streamlined execution mechanism.

## Why
CPUs and GPUs have discrete memory spaces. You gotta move data around and launch kernels. These things are costly.

## How
They implement persistent operators that continuously process data through shared topics, which establish efficient inter-processor data channels via hardware page faults.

## Notes

* They let hardware page faults rather than software invocations handle data transfer and overlapping.
* They only launch the kernel once and then compute input data throughout the whole running time.
* They use direct read for data synchronization. atomicAdd_system() to atomically update a concurrent UM variable.
* Another approach is to use CAS (compare and swap). A lock is initialized to 0. To acquire this lock, the caller repeats CAS until it swaps 1 to this lock variable succesfully.