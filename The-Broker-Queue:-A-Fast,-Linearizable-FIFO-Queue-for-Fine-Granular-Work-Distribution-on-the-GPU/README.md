# The Broker Queue

No available code as far as I can see.

## Notes

* The FIFO queue design, which defines a head from which items are drawn and a tail for appending items, is the most common choice in previous work.
* It implicitly maintains tasks in the order in which they were submitted. 
* Michael-Scott queue (MSQ) is one of the most popular lock-free concurrent queues ([Paper](https://www.cs.rochester.edu/~scott/papers/1996_PODC_queues.pdf)).
* Array-based queues employ a continuous array of elements, commonly operated as a ring buffer.
* In non-blocking queues, the high resource contention on the GPU — when thousands of threads try to access the same data element— can lead to a significant number of retries, e.g., hundreds to thousands of repeated CAS (compare-and-swap) operations for a single enqueue.


### Requirements of GPU Queues

* Scalability
* Fair Ordering
* Linearizability
* Low Resource Footprint
* Static Memory Only
* Suppor tfor All Execution Paradigms
* Multi-queue Support
* Multi-element Dequeue