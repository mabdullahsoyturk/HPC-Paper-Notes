# Alleviating Irregularity in Graph Analytics Acceleration: a Hardware Software Co-Design Approach
Reference: Mingyu Yan, Xing Hu, Shuangchen Li, Abanti Basak, Han Li, Xin Ma, Itir Akgun, Yujing Feng, Peng Gu, Lei Deng, Xiaochun Ye, Zhimin Zhang, Dongrui Fan, and Yuan Xie. 2019. Alleviating Irregularity in Graph Analytics Acceleration: a Hardware/Software Co-Design Approach. In Proceedings of the 52nd Annual IEEE/ACM International Symposium on Microarchitecture (MICRO ’52). Association for Computing Machinery, New York, NY, USA, 615–628. DOI:https://doi.org/10.1145/3352460.3358318

## Questions
- How do they achieve datapath decoupling?
- How do they perform data-aware dynamic scheduling?
- How do they extract the workload size?
- How do they extract the exact prefetching indication?

## Notes:

* Due to the data-dependent program behavior of graph algorithms, existing architectures face several challenges. Specifically, **imbalanced workloads**, large amounts of random memory accesses across diverse memory regions, and redundant computations result from the following three types of irregularities: 

1. Workload Irregularity: The workloads among threads are significantly imbalanced.
2. Traversal Irregularity: : Edges are traversed irregularly in each iteration. This is caused by the different active vertices among iterations and the irregular connections between active vertices and their neighbors.
3. Update Irregularity: Update of vertex property and activation of vertex vary each iteration. Although few vertices are updated and activated, the program needs to check all vertices.

## Main Question
Could we schedule the program by considering the data dependency in order to tackle these irregularities?

## Solution
A hardware/software co-design with **decoupled datapath** and **data-aware dynamic scheduling**.

## Decoupled Datapath
* Decoupled datapath is used to **extract the data dependency in microarchitecture level**
* A Dispatching/Processing programming model is proposed to **extract the workload size** as well as **the exact prefetching indication of the coming accessed data**.
* A microarchitecture design is also proposed to facilitate the decoupling of microarchitecture datapath.

## Data-aware Dynamic Scheduling
It is used to schedule the program on-the-fly by considering the data dependency. 

* To address **workload irregularity**, it dynamically dispatches workloads to processing elements in a balanced manner with knowledge of the precalculated workload sizes.
* To mitigate the **traversal irregularity**, we perform an exact prefetching to prefetch graph data with knowledge of the exact prefetching indication. (**Graphicinado** addresses this)
* To mitigate the **traversal irregularity**, a store-reduce mechanism with a microarchitectural pipeline, which dynamically schedules the read-after-write data access for eliminating any stalls caused by atomicity, is proposed.(Graphicinado does not address this)
* To mitigate **update irregularity**, it maintains a bitmap to record the ready-to-update vertices with the indication from the proposed pipeline. During the
update, only the marked vertices are scheduled to compute.

## Limitations of State of Art
* Graphicionado [24] partially addresses the traversal irregularity via an on-chip buffer to improve performance and energy efficiency.
* Graphicionado does not address the overhead of **atomics within the traversal irregularity**, **workload irregularity**, and **update irregularity**. 

* The workload irregularity leads to workload imbalance within pipeline. Because **active vertices possess more than ten neighbors on average**, the back-end of the pipeline has 10× more workload than the front-end. 

* Hash-based (i.e., random) workloads allocated to different pipelines lead to only half of the pipelines experiencing workloads most of the time. 

* Graphicionado **enforces atomicity by stalling the pipeline** when contention is detected. These stalls cause up to **20% additional execution time**. 

* Update irregularity results in **20% additional execution time** and **40% additional energy consumption**.

* In fact, these irregularities result from the data dependent program behavior, which relies on intermediate results within and across iterations.

## GraphDYNS
Includes: 

* Optimized programming model
* Hardware accelerator
* Data-aware dynamic scheduling strategies

### Optimized programming model
The optimizations include: 
* Determining the workload size during execution for scheduling a balanced workload
* Obtaining the prefetching indication during execution for exact prefetching
* Decoupling the phases into two pipeline stages to overlap workload scheduling and execution.

#### Dynamically Determining Workload Size
The key idea is to **determine the number of edges for each active vertex** by the offset array in the Apply phase, and use it in the Scatter phase of the next iteration.