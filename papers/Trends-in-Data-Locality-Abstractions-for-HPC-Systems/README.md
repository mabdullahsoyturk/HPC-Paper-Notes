# Trends in Data Locality Abstractions for HPC Systems

D. Unat et al., "Trends in Data Locality Abstractions for HPC Systems," in IEEE Transactions on Parallel and Distributed Systems, vol. 28, no. 10, pp. 3007-3020, 1 Oct. 2017, doi: 10.1109/TPDS.2017.2703149.

## Notes

* Energy efficiency of transistors is improving as their sizes shrink, but the energy efficiency of wires stays the same. So, communication cost becomes much more important than computation.
* The impact of data locality optimization has moved from being a tuning option to a central feature of code writing to get any performance improvement at all.
* They conducted a series of workshops on the topic of programming abstractions for data locality for high performance computing (HPC) that gather practitioners and researchers from all applicable areas. This paper explains the outcomes of these workshops.
* **Data Structure and Library Support**
  * **Algorithmic Execution Dependence**: They emphasize the usefulness of picking the best layout by analyzing the abstract algorithm instead of restructuring an existing code.
  * **Seperation of Concerns**: A well-defined separation of concerns clearly identifies who (library or application) is responsible for what. 
    * **What**: Mapping of data structures to memory spaces and algorithms to execution spaces.
* **Language and Compiler Support**
  * **Object Visibility**: Choice between local-by-default and global-by-default object visibility.
    * Local by default: MPI
    * Global by default: PGAS
  * **Requirements**: Abstractions need low overhead and high-level semantic information. 
* **Task-based Runtime Approaches**
  * **Runtime Involvement**
  * **Abstractions for Locality**
* **System-scale Data Locality Management**
  * **Trends and Requirements**: Even large networks have low diamaters. Therefore, topology mapping could become less important in some cases as the placement may have a smaller impact on the performance. In the case of very large machines such as top-end supercomputers featuring millions of cores, the algorithmic cost of process placement becomes very high. Another important consideration is the ability to deal with dynamic behavior.

