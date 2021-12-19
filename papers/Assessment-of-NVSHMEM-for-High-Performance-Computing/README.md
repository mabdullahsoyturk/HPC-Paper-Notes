# Assessment of NVSHMEM for High Performance Computing

C. Hsu, N. Imam, A. Langer, S. Potluri and C. J. Newburn, "An Initial Assessment of NVSHMEM for High Performance Computing," 2020 IEEE International Parallel and Distributed Processing Symposium Workshops (IPDPSW), 2020, pp. 1-10, doi: 10.1109/IPDPSW50202.2020.00104.

## What
Asssesment of NVSHMEM library.

## Why
NVSHMEM is a relatively new partitioned global address space programming model. Assessing it is useful in terms of usability, functionality, and scalability.

## How
They run two math kernels, matrix multiplication and Jacobi solver, and one full application (Horovod).

## Notes

* The PE uses one and only one GPU throughout the lifetime of an NVSHMEM job.
* **nvshmem_malloc** for symmetric heap allocation, malloc for normal allocation. **nvshmem_get** and **nvshmem_put** for memory accesses on symmetric heap.
* If a CUDA kernel in a PE calls NVSHMEM synchronization routines (such as **nvshmem wait**, **nvshmem barrier**, or **nvshmem barrier all**), then it is required to
be launched using nvshmemx collective launch routine.
* One-sided remote (atomic) memory access, memory ordering, point-to-point synchronization and collectives are supported from both the host and the GPU.
* Blocking get operations are not guaranteed to be in program order in NVSHMEM. A blocking get operation returns to the destination array at the local PE, after the data has been delivered. 
* NVSHMEM relaxes the ordering requirement of get operations and requires the programmer to use a fence where such ordering is required.