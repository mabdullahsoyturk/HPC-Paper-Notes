# Memory Bandwidth Contention: Communication vs Computation Tradeoffs in Supercomputers with Multicore Architectures

J. Langguth, X. Cai and M. Sourouri, "Memory Bandwidth Contention: Communication vs Computation Tradeoffs in Supercomputers with Multicore Architectures," 2018 IEEE 24th International Conference on Parallel and Distributed Systems (ICPADS), 2018, pp. 497-506, doi: 10.1109/PADSW.2018.8644601.

## Notes

* The problem is observed when communication and computation are overlapped, and both operations compete for the same memory bandwidth (computation should be memory-bound).

* The arithmetic performance grows faster than memory bandwidth (Check Intel Sandy Bridge vs Intel Broadwell).

* In most cases the impact of not using overlap is much higher than that of memory bandwidth contention.