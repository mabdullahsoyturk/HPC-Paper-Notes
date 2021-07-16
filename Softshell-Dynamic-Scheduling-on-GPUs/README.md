# Softshell

Code: [https://www.tugraz.at/institute/icg/research/team-schmalstieg/software/gpu-downloads/](https://www.tugraz.at/institute/icg/research/team-schmalstieg/software/gpu-downloads/)

## Notes

* Scheduling is a well-studied problem in operating system design area. It would be good to check some OS papers on this.
* There was no such thing as dynamic parallelism at the time this paper was written. Keep that it mind.
* Work can be issued on the device.
* Supports arbitrary scheduling stragies such as **dynamic priorities** and **real-time scheduling**.
* The user can influence, pause, and cancel work that is already submitted.


### Limitations of Traditional GPU Programming

* There is no way to adjust the parallelism during a single kernel launch (for example, you cannot change the number of threads after kernel launch).
* For good performance, kernels should be started with thousands of threads. This is too rigid for many algorithms such as tree algorithms that launch a kernel for each tree level. Also, tree depth may vary (this would cause work imbalance). The easier and more efficient solution would be to launch new threads for every child node dynamically.
* Kernel launches are controlled by the CPU. Unnecessary synchs and overheads. It's better launch them on the GPU. 
* No way to interrupt or terminate a running kernel (cause they run to completion).
* No work scheduling functionality on GPU (this is apparently a common practice on CPUs). Since GPU scheduling is FIFO, work-intensive background tasks can block the entire GPU. 