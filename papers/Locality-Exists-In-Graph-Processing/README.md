# Locality Exists in Graph Processing: Workload Characterization on an Ivy Bridge Serve 
Reference: "Locality Exists in Graph Processing: Workload Characterization on an Ivy Bridge Server", Scott Beamer, Krste Asanović, and David Patterson, International Symposium on Workload Characterization (IISWC), Atlanta, October 2015

## Learn more about the followings:


## Questions:

## Notes:

*  Graph algorithms struggle to fully utilize the platform’s memory bandwidth.
*  **Increasing memory bandwidth utilization** could be just as effective as **decreasing communication**.
*  Because message-passing is far less efficient than accessing memory in contemporary systems, distributed clusters are a poor match to graph processing.
*  The biggest memory bandwidth bottleck is the instruction window. 
*  Input graph has the largest impact on performance characteristics.
*  TLB misses are only detrimental when at least a moderate amount of memory bandwidth is utilized.
*  Branch misspredictions and unresolved data dependencies can also hinder memory bandwidth utilization.
*  Memory bandwidth is also moderately hindered by NUMA effects.

Some insights:
1. Graph apps exhibit substantial locality. They experience moderately high LLC hit rate.
2. Reorder buffer size limits achievable memory throughput. Relatively high LLC hit rate implies many instructions are executed for each LLC miss.These instructions fill the reorder buffer in the core, preventing future loads that will miss in the LLC from issuing early, resulting in unused memory bandwidth.
3. Multithreading has limited potential for graph processing


### Memory Bandwidth Potential
A load must satisfy the following four requirements:
1. Processor fetches load instruction.
2. Space in instruction window - Reorder Buffer (ROB) is not full and has room for the load.
3. Register operands are available.
4. Memory bandwidth is available - At the core level there is a MSHR available and there is not excessive contention within the on-chip interconnect or at the memory controller.

Memory bandwidth cannot be a bottleneck unless the first three requirements are satisfied.

* The biggest bandwidth bottleneck is the instruction window because it cannot hold a sufﬁcient number of instructions to incorporate the needed number of cache-missing instructions.