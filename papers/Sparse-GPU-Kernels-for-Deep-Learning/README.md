# Sparse GPU Kernels for Deep Learning

Gale, Trevor, et al. "Sparse gpu kernels for deep learning." SC20: International Conference for High Performance Computing, Networking, Storage and Analysis. IEEE, 2020.

## Notes

Link to code: [code](https://github.com/google-research/sputnik)

* Sparse matrix–matrix multiplication runtime for a weight-sparse long short-term memory network problem: Input size 8192, hidden size 2048, and batch size 128 in single-precision on an Nvidia V100 GPU. Sparse computation exceeds the performance of dense at as low as **71% sparsity**.