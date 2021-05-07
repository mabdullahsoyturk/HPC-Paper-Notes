# Fast and Scalable Sparse Triangular Solver forMulti-GPU Based HPC Architectures

## Questions

### What is SpTRSV?
Remember the linear algebra course. Given Lx = b or Ux = b where L is lower triangular, U is upper triangular matrix and b is a vector of values. We are seeking a solution for x.

### Why should I care about SpTRSV at all?
It's used in HPC apps such as numerical simulation, power grid simulation, computational chemistry, climate modeling etc.

### Why is it hard to design efficient and scalable sparse linear algebra kernels on multi-GPU systems?
* Irregular memory references
* Workload imbalances
* Computation dependencies (This dependency info is shared among GPUs)

### Why unified memory adversely affect the performance?
GPUs race for data to resolve dependencies and this cause Unified Memory's Page Migration Engine to create a ping pong effect. It moves the same pages back and forth. 

### How does NVSHMEM reduce synchronization overhead?
It supports one-sided get and put operations and P2P communication within the kernel. This also allows the overlapping of communication and computation.

## Notes
* They are trying to optimize SpTRSV (Sparse Triangular Solver). 
* They scale up (single node multiple GPUs). So, they partition the data and distribute to the GPUs.
* To calculate the dependencies, GPUs often need to share data. 


