# Productivity, Portability, Performance: Data-Centric Python

Ziogas, Alexandros Nikolaos, et al. "Productivity, Portability, Performance: Data-Centric Python." arXiv preprint arXiv:2107.00555 (2021).

## Notes

* I would recommend reading the [previous paper](../Stateful-Dataflow-Multigraphs-A-Data-Centric-Model-for-Performance-Portability-on-Heterogeneous-Architectures) before reading this paper.
* 3Ps: Productivity, Portability, Performance

**Productivity**: Provides a methodology to translate Python code to a data-centric IR, and extensions to improve said conversion via explicit annotation.

**Portability**: Automatic optimizations for CPU, GPU and FPGA.

**Performance**: Automatic MPI transformations and communication optimizations. It also facilitates explicit distribution management.

* Uses decorators to get dataflow graph.
* dace = **DA**ta **CE**ntric.

* Parses Python code and converts it to SDFGs on a per function basis.
* SDFGs should be statically typed.

![Example](figures/example.png)

* For parametric parallelism, either use dace.map or DaCe provides LoopToMap transformation on IR.

SDFG generation from a Python program:

```Python
@dace.program
def gemm (alpha, beta, C, A, B):
    C[:] = alpha * A @ B + beta * C
```

First pass traverses Python AST. Creates a SSA type of output.

```Python
tmp0 = alpha * A
tmp1 = tmp0 @ B
tmp2 = beta * C
C = tmp1 + tmp2
```

Then, they perform transformations on this (redundant copy removal, inlining etc.). As a performance engineer, you can say "don't perform these automatically, I will choose the ones that I want to apply manually".

### Automatic Optimization Heuristics

* All transformations either matching a subgraph pattern ([read this to learn about subgraph pattern matching](https://getd.libs.uga.edu/pdfs/saltz_matthew_w_201308_ms.pdf)) or allowing the user to choose an arbitrary subgraph.

* They only discuss results produced in an automated fashion which is good.

* Auto optimizer performs the following passes:
  - **Map scope cleanup**: Removes degenerate maps of size 1. Collapses nested maps together to form multidimensional maps.
  - **Greedy subgraph fusion**: Collects all maps in each state and fuses largest contiguous subgraphs that share the same iteration space.
  - **Tile WCR maps**: Tiles parallel maps with write-conflicts that result in atomics.
  - **Transient allocation mitigation**: Move constant-sized and small arrays to the stack, and make temporary data containers persistent if size only depends on input parameters.

  The rest is platform dependent optimizations.

### Library Specilization

Library Nodes, such as the MatMul operation in gemm , can be expanded to a wide variety of implementations. It is extendable.

### Ahead-of-Time Compilation

A decorated function or an SDFG can be directly compiled to a shared library.

The rest is results and dang they are really really good.