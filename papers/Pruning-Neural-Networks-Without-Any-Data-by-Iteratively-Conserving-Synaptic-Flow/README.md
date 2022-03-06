# Pruning neural networks without any data by iteratively conserving synaptic flow

Tanaka, Hidenori, et al. "Pruning neural networks without any data by iteratively conserving synaptic flow." Advances in Neural Information Processing Systems 33 (2020): 6377-6389.

## Notes

* The fundamental question: Can we identify highly sparse trainable subnetworks at initialization, without ever training, or indeed without ever looking at the data?
* Empirically, its been shown that global-masking performs far better than layer-masking, in part because it introduces fewer hyperparameters and allows for flexible pruning rates across the network
* Layer collapse might happen in global masking. Layer-collapse occurs when an algorithm prunes all parameters in a single weight layer even when prunable parameters remain elsewhere in the network