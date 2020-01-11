# Energy Efficient Architecture for Graph Analytics Accelerators

Reference: M. M. Ozdal et al., "Energy Efficient Architecture for Graph Analytics Accelerators," 2016 ACM/IEEE 43rd Annual International Symposium on Computer Architecture (ISCA), Seoul, 2016, pp. 166-177

## Learn about the following:
* Vertex-centric applications with irregular access patterns and asymmetric convergence.
* CPU vector extensions such as SSE and AVX.

## Questions:
* What does graph-parallel computation mean? 

It is similar to data-parallel computation. In data-parallel computation, we process **independent data** on **seperate resources**. In grap-parallel computation, we partition the graph data (**dependent**) across processing resources and then resolve the dependencies through iterative computation. 

## Notes:

* Many existing works focus on accelerating copute-intensive tasks using **programmable hardware** (GPUs, CPU vector extensions such SSE and AVX) or custom hardware. Common characteristic of these applications: regularity and thread level parallelism. 
* It is not convenient to use existing platforms for applications with **irregular execution patterns**.
* This paper focuses on **iterative graph-parallel** applications with **asynchronous execution** and **asymmetric convergence** 