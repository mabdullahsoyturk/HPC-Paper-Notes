# List of Papers

1. [Energy Efficient Architecture for Graph Analytics Accelerators](Energy-Efficient-Architecture-for-Graph-Analytics-Accelerators)
2. [A Template Based Design Methodology for Graph Parallel Hardware Accelerators](A-Template-Based-Design-Methodology-for-Graph-Parallel-Hardware-Accelerators)
3. [System Simulation with gem5 and SystemC](System-Simulation-with-gem5-and-SystemC)
4. [GAIL: The Graph Algorithm Iron Law](The-Graph-Algorithm-Iron-Law)
5. [Locality Exists in Graph Processing: Workload Characterization on an Ivy Bridge Serve](Locality-Exists-In-Graph-Processing)
6. [Graphicionado A High Performance and Energy-Efficient Accelerator for Graph Analytics](Graphicionado-A-High-Performance-and-Energy-Efficient-Accelerator-for-Graph-Analytics)
7. [Analysis and Optimization of the Memory Hierarchy for Graph Processing Workloads](Analysis-and-Optimization-of-the-Memory-Hierarchy-for-Graph-Processing-Workloads)
8. [Alleviating Irregularity in Graph Analytics Acceleration: a Hardware/Software Design Approach](Alleviating-Irregularity-in-Graph-Analytics-Acceleration)
9. [GNN Performance Optimization](GNN-Performance-Optimization)
10. [Dissecting the Graphcore IPU Architecture](Dissecting-the-Graphcore-IPU-Architecture)
11. [Using the Graphcore IPU for Traditional HPC Applications](Using-the-Graphcore-IPU-for-Traditional-HPC-Applications)
12. [Roofline: An Insightful Visual Performance Model](Roofline-An-Insightful-Visual-Performance-Model)
13. [CUDA New Features and Beyond](CUDA-New-Features-and-Beyond)
14. [A Study of Persistent Threads Style GPU Programming for GPGPU Workloads](A-Study-of-Persistent-Threads-Style-GPU-Programming-for-GPGPU-Workloads)
15. [BrainTorrent: A Peer to Peer Environment for Decentralized Federated Learning](BrainTorrent-A-Peer-to-Peer-Environment-for-Decentralized-Federated-Learning)
16. [Whippletree: Task-based Scheduling of Dynamic Workloads on the GPU](./Whippletree:Task-based-Scheduling-of-Dynamic-Workloads-on-the-GPU)
17. [Groute: Asynchronous Multi-GPU Programming Model with Applications to Large-scale Graph Processing](./Groute:Asynchronous-Multi-GPU-Programming-Model-with-Applications-to-Large-scale-Graph-Processing)

## Two Papers A Week Goal (Starting from 28.06.2021)

### 28.06.2021 - 04.07.2021

* [Whippletree: Task-based Scheduling of Dynamic Workloads on the GPU](Whippletree-Task-based-Scheduling-of-Dynamic-Workloads-on-the-GPU)
* [Groute: Asynchronous Multi-GPU Programming Model with Applications to Large-scale Graph Processing](Groute-Asynchronous-Multi-GPU-Programming-Model-with-Applications-to-Large-scale-Graph-Processing)

### 05.07.2021 - 11.07.2021

* [A Computational-Graph Partitioning Method for Training Memory-Constrained DNNs](A-Computational-Graph-Partitioning-Method-for-Training-Memory-Constrained-DNNs)
* [The Broker Queue: A Fast, Linearizable FIFO Queue for Fine-Granular Work Distribution on the GPU](The-Broker-Queue-A-Fast-Linearizable-FIFO-Queue-for-Fine-Granular-Work-Distribution-on-the-GPU)

### 12.07.2021 - 18.07.2021

* [Softshell: Dynamic Scheduling on GPUs](Softshell-Dynamic-Scheduling-on-GPUs)
* [Gravel: Fine-Grain GPU-Initiated Network Messages](Gravel-Fine-Grain-GPU-Initiated-Network-Messages)

## Potential Readings

* [Softshell: Dynamic Scheduling on GPUs](Softshell:-Dynamic-Scheduling-on-GPUs)
* [Gravel: Fine-Grain GPU-Initiated Network Messages](https://research.cs.wisc.edu/multifacet/papers/sc17_gravel.pdf)
* [Ouroboros: Virtualized Queues for Dynamic Memory Management on GPUs](Ouroboros:-Virtualized-Queues-for-Dynamic-Memory-Management-on-GPUs)
* [DynaSOAr: A CUDA Framework for Single-Method Multiple-Objects Applications](https://github.com/prg-titech/dynasoar)
* [LaPerm: Locality Aware Scheduler for Dynamic Parallelism on GPUs](https://ieeexplore.ieee.org/document/7551424)
* [Dynamic Task Parallelism with a GPU Work-Stealing Runtime System](Dynamic-Task-Parallelism-with-a-GPU-Work-Stealing)

### Coprocessor Model

Disallows GPUs to access NI. You write CPU code for communication before and after a GPU kernel.

* [Efficient Inter-Node MPI Communication Using GPUDirect RDMA for InfiniBand Clusters with NVIDIA GPUs](https://ieeexplore.ieee.org/document/6687341) -> CUDA RDMA
* [Optimized GPU to GPU Communication for InfiniBand Clusters](https://link.springer.com/article/10.1007/s00450-011-0171-3) -> CUDA-aware MPI

### Message-per-lane Model

GPU threads independently access to NI. 

* [GGAS: Global GPU Address Spaces for Efficient Communication in Heterogeneous Clusters](https://ieeexplore.ieee.org/document/6702638)
* [Simplifying Multi-GPU Communication with NVSHMEM](http://on-demand.gputechconf.com/gtc/2016/presentation/s6378-nathan-luehr-simplyfing-multi-gpu-communication-nvshmem.pdf) -> Not a paper but good to read.

### Coalesced APIs

WIs coordinate with their neighbors to access the NI

* [GPUnet: Networking Abstractions for GPU Programs](https://www.usenix.org/system/files/conference/osdi14/osdi14-paper-kim.pdf)
* [GPUrdma: GPU-Side Library for High Performance Networking from GPU Kernels](https://dl.acm.org/doi/10.1145/2931088.2931091)