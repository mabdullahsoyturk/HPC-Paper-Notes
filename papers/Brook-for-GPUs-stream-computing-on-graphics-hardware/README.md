# Brook for GPUs: Stream Computing on Graphics Hardware

Ian Buck, Tim Foley, Daniel Horn, Jeremy Sugerman, Kayvon Fatahalian, Mike Houston, and Pat Hanrahan. 2004. Brook for GPUs: stream computing on graphics hardware. ACM Trans. Graph. 23, 3 (August 2004), 777–786. DOI:https://doi.org/10.1145/1015706.1015800

## Notes

* Looks very similar to CUDA. 
* Supports three backends: OpenGL, DirectX and a CPU implementation for reference.
* They implement a compiler (brcc) and a runtime (BRT). The compiler maps Brook kernels into Cg shaders (Cg is a legacy toolkit of NVIDIA before CUDA).