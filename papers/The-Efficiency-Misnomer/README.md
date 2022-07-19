# The Efficiency Misnomer

@inproceedings{
dehghani2022the,
title={The Efficiency Misnomer},
author={Mostafa Dehghani and Yi Tay and Anurag Arnab and Lucas Beyer and Ashish Vaswani},
booktitle={International Conference on Learning Representations},
year={2022},
url={https://openreview.net/forum?id=iulEMLYh1uR}
}

## Notes

* **Commonly Used Cost Indicators**:
  * FLOPs: A proxy for the computational cost of a model. Calculates the number of floating-point multiplication-and-addition operations. Theoretical FLOPs ignores practical factors, like which parts of the model can be parallelized.
  * Number of parameters: Used as an indirect indicator of computational complexity as well as memory usage (during inference). Especially, NLP papers use this as the primary cost indicator very often.
  * Speed: Strongly depends on hardware and implementation, so keeping the hardware fixed or normalizing based on the amount of resources used is the key for a fair comparison.
    * Throughtput: Tokens/Second
    * Latency: Seconds per forward pass
    * Runtime: Time to convergence
    * Pipeline Bubble: Computing devices are idle at the start and end of every batch (Narayanan et al., 2021), which indirectly measures the speed of the non-pipeline parts of the process.
    * Memory Access Cost (MAC): Corresponds to number of memory accessses. It typically makes up a large portion of runtime and is the actual bottleneck.

* Sparse models result in large reductions in theoretical FLOPs, often of several orders of magnitude but these do not translate to equally large speed-ups because sparse kernels cannot use modern hardware efficiently (e.g. lots of cache misses)
* Sparse models remain compute-matched while enabling scaling to a large number of parameters. Hence, parameter matched comparisons do not make sense for sparse models and parameter-matching sparse models can be seen as an unfair method of unnecessarily downplaying
the strengths of sparse models. Many works in the literature employ compute-matched comparisons for comparing sparse models (Narang et al., 2021; Fedus et al., 2021; Lample et al., 2019).