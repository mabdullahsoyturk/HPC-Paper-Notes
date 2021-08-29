# Productivity, Portability, Performance: Data-Centric Python

Ziogas, Alexandros Nikolaos, et al. "Productivity, Portability, Performance: Data-Centric Python." arXiv preprint arXiv:2107.00555 (2021).

## Notes

* 3Ps: Productivity, Portability, Performance

**Productivity**: Provides a methodology to translate Python code to a data-centric IR, and extensions to improve said conversion via explicit annotation.

**Portability**: Automatic optimizations for CPU, GPU and FPGA.

**Performance**: Automatic MPI transformations and communication optimizations. It also facilitates explicit distribution management.

* Uses decorators to get dataflow graph.
* dace = **DA**ta **CE**ntric.

* Parses Python code and converts it to SDFGs on a per function basis.