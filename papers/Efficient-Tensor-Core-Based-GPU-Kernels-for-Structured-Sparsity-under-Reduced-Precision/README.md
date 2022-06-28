# Notes

* cuBLASHgemm -> Half precision GEMM. 
* They propose SpMM and SDDMM kernels and achieve 1.71-7.19x speedup over cuSPARSE.
* Achieves speed up over cuBLASHgemm under >70% and >90% sparsity with 4x1 grain size and half-precision.
* Existing implementations are insufficient for achieving practical speedup over their dense counterparts in half precision (FP16).
  * After using FP16, fast memory can cache more operands to improve data reuse, which is fully exploited by dense GEMM kernels. Whereas, fine-grained sparse kernels with much lower data reuse fail to exploit this benefit.
  * Although structured sparsity can be introduced to improve data reuse, existing libraries like cuSPARSE cannot deliver practical speedup with small sparsity granularity.
  * As you increase the sparsity granularity, it is harder to maintain accuracy.
* Consecutive 4 threads in a warp is called **thread group**. Thread group id: (threadIdx % 32) / 4.
* Thread group i (0,1,2,3) and thread group i+4 (16,17,18,19) together form **Octet** i. i is the low group and i+4 is the high group.
* LDG 128 can be used to increase the sectors per request to L1 Cache. 128 means each thread reads 128 bits from the global memory (e.g. 8 operands under the half precision).
* A warp uses 2 TCUs at the same time. Each TCU is controlled by two octets.
* Two levels of APIs for TCU:
  * Warp-level matrix multiply and accumulate (WMMA) performs dense MM with a warp. wmma.m8n32k16 computes (8x16).(16x32) GEMM with a warp.
  * Matrix multiply and accumulate in PTX performs 4 dense MM with a warp, one for each octet. mma.m8n8k4 computes four (8x4).(4x8) MMs.