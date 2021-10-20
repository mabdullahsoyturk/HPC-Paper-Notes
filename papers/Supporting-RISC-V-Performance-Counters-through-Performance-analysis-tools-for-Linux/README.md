# Supporting RISC-V Performance Counters through Performance analysis tools for Linux

JOAO MARIO DOMINGOS, PEDRO TOMAS, and LEONEL SOUSA

## What

Extensions and modifications to the performance analysis tools for Linux (perf/perf_events), Linux kernel, and OpenSBI.

## Why

* Linux Perf cannot write to the counters and event configuration registers since it requires machine-level privilege.
* So that apps can be optimized better.

## How

By introducing a new OpenSBI extension.

## Notes

* RISC-V is still not fully supported in the Linux kernel monitoring tool Perf.
* Linux Perf implementation is not capable of writing to counters and event configuration register because it require machine level privilege which is not available without a dedicated OpenSBI extension. Therefore, you can't configure events in a specific counter.

### Some Terminology

OpenSBI = Open Source Supervisor Binary Interface
CTI Instructions = Cycle, Time and Retired Instructions
PMU = Performance Monitoring Unit
HPM = High Performance Monitor
