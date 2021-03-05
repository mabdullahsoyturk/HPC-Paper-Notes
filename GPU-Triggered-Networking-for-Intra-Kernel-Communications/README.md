## Notes

* While many clusters employ peer-to-peer capabilities for direct data movement between NICs and GPUs, the control plane is routed through the host CPU. This restricts communication to only occur on GPU kernel boundaries (Host-driven Networking (HDN)).
*  GPUDirect Async (GDS) is one of the HDNs. It allows the GPU to initiate pre-registered network messages by ringing a doorbell on the NIC.
*  