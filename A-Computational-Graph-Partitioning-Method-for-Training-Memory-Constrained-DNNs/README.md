# PARDNN

## Notes

Two steps:

1. Cluster operation nodes of the computational graph into K (number of devices) partitions.
2. Check whether memory constraints are met in each partition. If not, reassign.

Scheduling length = makespan = Completion time (C_t) of the last node. 

* C_t(n) is the time required to execute the operation represented by n added to the time at which this operation starts to execute.
* Goal is to minimize C_tmax = max C_t(n) for n in V (Vertices of the graph).

ParDNN inputs:

* **Device count**
* **Device memory capacities**
* **Interconnection bandwidth and latency**
* **DAG of computations**
* **Profiling data**: Execution time measurements, size of the output of each operation node. Tensorflow standard API gives per-node time, memory consumption, and communication sizes at the granularity of graph nodes for regular as well as user-defined operators. To estimate the memory consumption, they implement an emulator of TensorFlow’s scheduler.
* **Operations metada**: Operation types.

ParDNN outputs:
* Outputs a mapping of operations to devices. You feed that to the Tensorflow execution engine.
