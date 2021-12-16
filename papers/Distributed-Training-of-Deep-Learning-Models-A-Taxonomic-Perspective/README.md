# Distributed Training of Deep Learning Models:A Taxonomic Perspective

Langer, Matthias, et al. "Distributed training of deep learning models: A taxonomic perspective." IEEE Transactions on Parallel and Distributed Systems 31.12 (2020): 2802-2818.

## What

An overview on distributed deep learning systems (DDLS).

## Why

There are various ways to train models on a distributed environment. Developers should pick the one that suits well to their system. 

## How

They create a taxonomy by assorting the fundamental characteristics that have a major impact on how DDLS operate.

## Notes

* Taxonomy is split into 4 sections: 
  - Model vs. data parallelism
  - Centralized vs. decentralized optimization
  - Synchronous vs. asynchronous scheduling
  - The communication pattern used for exchanging parameters

* Apparently, in this paper they call forward pass inference. Kinda strange but ok.

* The key idea behind decentralized optimization is that multiple independent entities concurrently try to solve a similar but not exactly the same problem. Because the loss
function in deep learning is independent, numeric optimizers that observe the loss function at different locations eventually find different descent trails more appealing and converge towards different local minima. Hence, over time, the workers diverge and eventually arrive at incompatible models (i. e. models that cannot be merged without destroying the accumulated information). Therefore, DDLS that rely on decentralized optimization have to take measures to limit divergence.

* Decentralized: Exploration + Exploitation.

* Short exploration phases may not allow the workers to sufficiently probe the loss function to gather information, while long exploration phases lead to increased inconsistencies, which can hinder overall progress.