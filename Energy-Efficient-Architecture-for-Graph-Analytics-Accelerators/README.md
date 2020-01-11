# Energy Efficient Architecture for Graph Analytics Accelerators

Reference: M. M. Ozdal et al., "Energy Efficient Architecture for Graph Analytics Accelerators," 2016 ACM/IEEE 43rd Annual International Symposium on Computer Architecture (ISCA), Seoul, 2016, pp. 166-177

## Learn more about the followings:
* Vertex-centric applications with irregular access patterns and asymmetric convergence.
* CPU vector extensions such as SSE and AVX.
* GraphLab (Done)
* SystemC
* Memory level parallelism
* Outstanding memory requests and MSHRs

## Questions:
* What does graph-parallel computation mean? 
* What is vertex-centric abstraction model?

It is similar to data-parallel computation. In data-parallel computation, we process **independent data** on **seperate resources**. In grap-parallel computation, we partition the graph data (**dependent**) across processing resources and then resolve the dependencies through iterative computation. 

## Notes:

* Many existing works focus on accelerating compute-intensive tasks using **programmable hardware** (GPUs, CPU vector extensions such SSE and AVX) or custom hardware. Common characteristic of these applications: regularity and thread level parallelism. 
* It is not convenient to use existing platforms for applications with **irregular execution patterns**.
* This paper focuses on **iterative graph-parallel** applications with **asynchronous execution** and **asymmetric convergence** 
* This kind of applications can be represented with a **vertex-centric abstraction model**. 
* **GraphLab** is an abstraction model to make it easy for domain experts to develop parallel and distributed programs.
* Objective of the paper is to create an abstraction model similar to **GraphLab** but targeted for architecture and hardware development of graph analytics accelerators.
* Authors propose a customaziable architecture template that is specifically optimized for the target class of graph applications.
* The architects plug in application-level data structures and operations into the template and generate the hardware implementation.

### Contributions
* An architecture specifically optimized for vertex-centric, iterative, graph-parallel applications with irregular access patterns and asymmetric convergence.
* Cycle-accurate and synthesizable SystemC models that implement the proposed architecture template.
* An experimental study that compares the **area, power, and performance** of the generated hardware accelerators with CPU implementations.

### Characteristics of Irregular Graph Applications

#### Asymmetric Convergence
The number of iterations each vertex needs to be processed before convergence may vary significantly.

#### Async Execution
Async execution often converges much faster than synch execution but it may converge slower for some applications because of potential synchronization overheads (Race conditions).

#### Memory Access Bottlenecks
* A vertex/edge processed is unlikely to be processed again before most of the other vertices/edges are processed (poor temporal locality).

* For real life unstructured graphs, the data of neighboring vertices are unlikely to be in the same cache lines (poor spatial locality).

#### Load Imbalance
Small percent of vertices cover most of the edges. 

### Limitations of General Purpose CPUs
* Memory latency is the main performance bottleneck.
* Low memory level parallelism (MLP) leads to under-utilization of the DRAM bandwidth.
* Overall performance scales linearly with memory bandwidth consumption because of overlapped access latencies.
