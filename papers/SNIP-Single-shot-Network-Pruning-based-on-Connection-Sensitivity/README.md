# SNIP: Single-shot Network Pruning based on Connection Sensitivity

Lee, Namhoon, Thalaiyasingam Ajanthan, and Philip HS Torr. "Snip: Single-shot network pruning based on connection sensitivity." arXiv preprint arXiv:1810.02340 (2018).

## Notes

* Previous works require many expensive prune – retrain cycles since pruning is included as a part of an iterative optimization procedure.
* They introduce a saliency criterion that identifies connections in the network that are important to the given task in a data-dependent way **before training**
* They discover important connections based on their influence on the loss function at a variance scaling initialization, which they call **connection sensitivity**.
* They do one forward and one backward pass, then keep top-k entries based on the magnitude of derivatives (this is the saliency criterion).
* They show that using only one mini-batch of a reasonable number of training examples can lead to effective pruning.
* The sensitivity scores are computed using a batch of 100 and 128 examples for MNIST and CIFAR experiments, respectively