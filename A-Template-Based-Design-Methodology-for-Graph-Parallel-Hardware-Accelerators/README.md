# A Template Based Design Methodology for Graph Parallel Hardware Accelerators

Reference: A. Ayupov, S. Yesil, M. M. Ozdal, T. Kim, S. Burns and O. Ozturk, "A Template-Based Design Methodology for Graph-Parallel Hardware Accelerators," in IEEE Transactions on Computer-Aided Design of Integrated Circuits and Systems, vol. 37, no. 2, pp. 420-430, Feb. 2018.
doi: 10.1109/TCAD.2017.2706562

## Learn more about the followings:
* IBM's wire-speed processor.


## Questions:

## Notes:
Graph analysis is different from traditional grid based high performance computing because of:
* Irregular communication
* Little data locality
* Low computation to communication ratio
* Frequent synchronization requirements
* Hard-to-predict work assignment.

Performance bottleneck for of big data graph applications typically the **DRAM access latency** due to **low compute-to-memory ratios** and **random memory access patterns**.

Most previous works on hardware accelerators assume that data resides in local memory with fixed latency. This is ensured by processing one partition at a time and overlapping **computation of the current partition** with the **communication of the next partition**. This is impractical for big data apps due to poor temporal/spatial locality.

* Due to aforementioned reasons, an accelerator for graph apps is expected to generate many concurrent DRAM requests to fully utilize DRAM bandwidth. 
