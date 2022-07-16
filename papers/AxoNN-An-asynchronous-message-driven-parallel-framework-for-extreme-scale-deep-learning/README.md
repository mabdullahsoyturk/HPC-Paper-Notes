# AxoNN: An asynchronous, message-driven parallel framework for extreme-scale deep learning

Singh, Siddharth, and Abhinav Bhatele. "Myelin: An asynchronous, message-driven parallel framework for extreme-scale deep learning." arXiv preprint arXiv:2110.13005 (2021).

## Notes

* Mixed precision: Keeps two copies of the network parameters in **single** and **half** precision. Forward and backward are done in **half** precision. Optimizer step is applied to **single** precision.
* Data parallelism: Has the restriction to fit the entire model into one GPU.
* Intra-layer parallelism: Prohibited by expensive collective calls. Use it in a node with high speed interconnects. Don't try to scale it to multiple nodes.
* Inter-layer parallelism: Pipeline stalls.