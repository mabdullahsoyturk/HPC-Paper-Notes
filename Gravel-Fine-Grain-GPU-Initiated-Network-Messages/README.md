# Gravel: Fine-Grain GPU-Initiated Network Messages

Marc S. Orr, Shuai Che, Bradford M. Beckmann, Mark Oskin, Steven K. Reinhardt, and David A. Wood. 2017. Gravel: fine-grain GPU-initiated network messages. In Proceedings of the International Conference for High Performance Computing, Networking, Storage and Analysis (SC '17). Association for Computing Machinery, New York, NY, USA, Article 23, 1–12. DOI:https://doi.org/10.1145/3126908.3126914

## Learn more about this stuff

* PGAS (Partitioned Global Address Space) style communication

## Notes

* GPU-initiated communication is inefficient for small messages.
* Gravel offloads GPU-initiated messages through a GPU-queue to an aggregator.
* Aggregator is implemented with CPU threads.

### Challeneges about routing a message from a GPU thread to Network Interface

1. Network Inteface access coordination: A dependency between WIs executing in lockstep can cause deadlock.
2. Cost of producer/consumer synchronization: For example, in a graph algorithm it is typical to initiate a small message (e.g., a few bytes) every time a vertex’s neighbor resides on a different machine.


### Three programming abstraction proposals

1. **Coprocessor model**: Disallows GPUs to access NI. You write CPU code for communication before and after a GPU kernel.
2. **Message-per-lane model**: GPU threads independently access to NI. It may generate small, high-overhead messages.
3. **Coalesced APIs**: WIs coordinate with their neighbors to access the NI. Harder to program, but it uses adjacent WIs to form larger messages (larger than message-per-lane, smaller than coprocessor).

### Terminologies and abbreviations used in the paper

* GPU thread = work item (WI)
* Network Interface = NI

