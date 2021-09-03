# Stateful Dataflow Multigraphs: A Data-Centric Model for Performance Portability on Heterogeneous Architectures

Ben-Nun, Tal, et al. "Stateful dataflow multigraphs: A data-centric model for performance portability on heterogeneous architectures." Proceedings of the International Conference for High Performance Computing, Networking, Storage and Analysis. 2019.

## Notes

![Scheme](./figures/scheme.png)

* **Performance Portable** means: Domain scientist's view does not change while the code is optimized to different target architectures.
* It bases on the observation that data-movement dominates time and energy in today’s computing systems.
* Extends existing data-centric mappers with:
  * A multi-level visualization of data movement
  * Code transformation and compilation for heterogeneous targets 
  * Strict separation of concerns for programming roles.

1. The domain programmer works in a convenient and well-known language such as Python. 
2. The compiler transforms the code into an SDFG.
3. Performance engineer works on SDFG, specifying transformations that match certain data-flow structures on all levels (from registers to inter-node communication) and modify them.

### Difference between dataflow and data-centric parallel programming

* Dataflow model execution is stateless (constructs such as loops have to be unrolled).
* Data-centric parallel programming uses **stateful dataflow**. Execution order depends on **data dependencies** and **global execution state**.

* Data-centric model combines the following concepts:
  * Seperating containers from computation (data holding constructs are defined as seperate entities from computations).
  * Dataflow (Information moving from one container to another)
  * States (Constructs that provide a mechanism to introduce execution order independent of data movement)
  * Coarsening (The ability to view parallel patterns in a hierarchical manner, e.g., by grouping repeating computations)

