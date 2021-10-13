# Benchmarking GPUs to Tune Dense Linear Algebra

V. Volkov and J. W. Demmel, "Benchmarking GPUs to tune dense linear algebra," SC '08: Proceedings of the 2008 ACM/IEEE Conference on Supercomputing, 2008, pp. 1-11, doi: 10.1109/SC.2008.5214359.

## Notes

* Reveals the structure of the GPU memory system, including sizes and latencies of the L1 and L2 caches and TLB.
* They implement and measure the performance of a global barrier that runs entirely on the GPU.

### Strip Mining on GPU

* Strip mining on GPU is done to improve performance in branching — associating an individual program counter with a short subset of a long vector allows skipping branches not taken by this subset rather than masking them off.

Potential problems of strip mining:

* It is expensive as it requires replicating register data across all instruction streams in the thread. For example, a program operating on 512-element vectors consumes 2KB of register file per every pointer, temporary value or scalar value defined in the scalar thread as a 32-bit register variable.
* The partitioning of the register data into private register spaces associated with different instruction streams in the thread. Accessing the data residing in
the register space of another warp requires staging it via the local store, which incurs costs.

Conclusion:

* One should use as short vectors as possible to avoid the extra costs associated with spreading the data across many warps but if you use a very short vector, then you compromise from the throughput. So, there needs to be a sweat spot for the number of threads in a warp which is still 32 at the momemnt for modern NVIDIA GPUs.

### Microbenchmarks

* They show the latency of kernel launch (3-7 us) by asynchronously invoking the same kernel a very large number of times and synchronizing once at the end. The program used was the simplest possible, such as copying one word from one location in the GPU memory to another. This ensures that the program runtime does not contribute substantially to the overall time. The time increases to 10–14 us when synchronizing at each kernel invocation. This shows the expense of synchronization.
* They use pointer chasing benchmark to reveal latency and structure of the memory system.
* To implement a global barrier on GPU, they replicate sych variables across the entire thread array. One arrival and one wakeup variable for each vector thread. The first vector is master, others are slaves. The i'th slave updates the i'th arrival variable and spins on the i'th wakeup variable until it is updated. The master spins on the arrival variables until they all are updated, then updates every wakeup variable.
* This implementation of global barrier **does not guarantee memory consistency** in all levels of memory hierarchy.

### Terminology

LU = Lower x Upper
QR = Orthogonal Matrix (Q) x Upper Triangular Matrix (R)
Cholesky = Lower Triangular x Its conjugate transpose
