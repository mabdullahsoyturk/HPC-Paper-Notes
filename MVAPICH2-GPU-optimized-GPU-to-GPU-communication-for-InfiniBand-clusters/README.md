# MVAPICH2-GPU: optimized GPU to GPU communication for InfiniBand clusters

Wang, H., Potluri, S., Luo, M. et al. MVAPICH2-GPU: optimized GPU to GPU communication for InfiniBand clusters. Comput Sci Res Dev 26, 257 (2011). https://doi.org/10.1007/s00450-011-0171-3

## Notes

* The problem was that developers were not able to register GPU addresses to MPI calls at that time.
* MVAPICH2-GPU solves that problem.

### Infiniband

* Allows Remote Direct Memory Access (RDMA)
* Requires communication buffers to be registered. 
* Host Channel Adapter (HCA) keeps the translation of virtual addresses to physical page locations.
* Due to a limitation in the Linux kernel, it is not possible for two PCI devices to register the same page.
* GPU-Direct is a Linux patch to solve this problem. Using GPU Direct, both network adapter and GPU can pin down the same buffer. 

Without GPU-Direct:

GPU memory -> Host memory for GPU -> Host memory for Infiniband -> Infiniband Network

With GPU-Direct:

GPU memory -> Host memory -> Infiniband Network

### MPI on Infiniband

* MVAPICH2 implements P2P using RDMA.

RDMA-put mechanism:

RTS        ----------------------> <br>
           <---------------------- CTS <br>
RDMA       ----------------------> <br>
RDMA Finished ------------------->

* One-sided communication allows apps to access remote memory directly.

One-sided communication mechanism:

Create a memory window -> perform one-sided writes and reads -> synchronize

### MVAPICH2-GPU interface

Most MPI implementations use the rendezvous protocol to handle large message transfers. 

* Target process provides the source with destination address information through a handshake. Then, source process writes to this address and notifies the target process when completed.

* MVAPICH2 pipelines GPU memory to host memory, network, and host memory to GPU memory (on remote side).

```C
if(rank == 0) {
    MPI_Send(device_buffer, size, MPI_CHAR, 1, 1, MPI_COMM_WORLD);
}else if(rank == 1) {
    MPI_Recv(receive_buffer, size, MPI_CHAR, 0, 1, MPI_COMM_WORLD, &reqstat);
}
```

In case one GPU buffer needs to be send to remote GPU device:

1. Sender sends RTS
2. Recv replies with CTS. Receiver encodes the remote buffer address and the size of the message to be received in the CTS.
3. The data is internally buffered (vbuf) at the sender and receiver host memory. The address encoded in the CTS message is a list of vbufs.
4. When the CTS is received by the sender, it starts async CUDA memory copy from D2H for each block (pipeline unit). The MPI library uses CUDA stream query function to check the status of each asynchronous memory copy.  
5. Once one of the asynchronous memory copies finishes, the sender calls InfiniBand verbs  nterface to perform the RDMA write.
6. After each RDMA write finishes, the sender sends out a RDMA write finish message.
7. When the receiver gets the RDMA write finish message, it starts the asynchronous CUDA memcpy to copy data from a vbuf to GPU device memory.

