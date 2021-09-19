# GGAS: Global GPU Address Spaces for Efficient Communication in Heterogeneous Clusters

L. Oden and H. Fröning, "GGAS: Global GPU address spaces for efficient communication in heterogeneous clusters," 2013 IEEE International Conference on Cluster Computing (CLUSTER), 2013, pp. 1-8, doi: 10.1109/CLUSTER.2013.6702638.

## Notes

GGAS style one GPU writing to the memory of another GPU.

```Cpp
__device__ remote_write (double val, int GPU, int index) {
    double* ptr = __ggas_get_ptr_of_node (GPU);
    ptr[index] = val;
}
```

* Although modern RDMA-capable hardware like Infiniband is able to transfer the data independently, still the CPU has to create send and receive requests and guarantee data consistency by synchronizing data transfer and computation.
* Context switching between GPU and CPU causes latency
issues. Especially for small messages, this can easily surpass the raw data transfer latency.

The launch and synchronization times for different GPUs (each kernel is started with 32 blocks of 32 threads):

GPU | Tesla K20 | Tesla K10 | Quadro FX 5800 | Quadro 2000
--- | --- | --- | --- | --- 
Time (us) | 13.5 | 13.4 | 13.78 | 9.4

Data transfer time over Infiniband:

Size (byte) | 2 | 16 | 1k | 4k | 32k | 64k
--- | --- | --- | --- | --- | --- | ---
Time (us) | 1.33 | 1.36 | 3.50 | 4.95 | 13.57 | 23.39

* GPU Direct RDMA is needed for the implementation.
* They use something called "Shared Memory Engine" to create the global address space. 