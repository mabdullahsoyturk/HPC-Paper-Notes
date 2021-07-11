# The Broker Queue

No available code as far as I can see.

## Notes

* FIFO queue is commonly used (draw items from head and append to tail)
* It implicitly maintains tasks in the order in which they were submitted. 
* Michael-Scott queue (MSQ) is one of the most popular lock-free concurrent queues ([Paper](https://www.cs.rochester.edu/~scott/papers/1996_PODC_queues.pdf)).
* Array-based queues employ a continuous array of elements, commonly operated as a circular queue (i.e. ring buffer).
* In non-blocking queues, the high resource contention on the GPU — when thousands of threads try to access the same data element— can lead to a significant number of retries, e.g., hundreds to thousands of repeated CAS (compare-and-swap) operations for a single enqueue.
* For scalability, blocking queues are preferable because of the reason in the previous bullet point.
* Every thread has to be assigned a unique spot in the queue to avoid retries on failed CAS operations. This leads to an array-based queue design, using atomic fetch-and-add (FAA) instead of CAS.

### Requirements of GPU Queues

* **Scalability**
* **Fair Ordering**: I didn't get the ticketing system.
* **Linearizability**
* **Low Resource Footprint**
* **Static Memory Only**: Large numbers of dynamic memory management operations are known to be a potential bottleneck for GPU execution. Using static memory only avoids this problem.
* **Support for All Execution Paradigms**: Should support independent thread execution, warp-synchronous execution, sub-block execution, and cooperative block execution etc.
* **Multi-queue Support**: Multi-queue setups require threads to eventually return from dequeue operations if a queue is already empty, so they can probe other queues for available data.
* **Multi-element Dequeue**


## Broker Queue

Four components:

1. A ring buffer for directly storing elements
2. A head and a tail pointer for ticketing
3. A ticket buffer that locks individual queue elements
4. An explicit counter to weigh enqueue against dequeue operations

For the rest of the paper, there is no point of taking notes. Check the code snippet provided in the paper to understand what's going on.