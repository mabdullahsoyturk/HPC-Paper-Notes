# The Lottery Ticket Hypothesis: Finding Sparse, Trainable Neural Networks

Frankle, Jonathan, and Michael Carbin. "The lottery ticket hypothesis: Finding sparse, trainable neural networks." arXiv preprint arXiv:1803.03635 (2018).

## Notes

* They show that smaller subnetworks can train as fast as the whole network while reaching similar test accuracy.
* **Lottery Ticket Hypothesis**: A randomly-initialized, dense neural network contains a subnetwork that is initialized such that —when trained in isolation— it can match the test accuracy of the original network after training for at most the same number of iterations.
* Let's say we have a model **f(x, w)**. When optimizing with SGD, f reaches minimum validation loss **l** at iteration **j** with test accuracy **a**. Consider training f(x, m x w) with mask **m is {0, 1}**.  When optimizing with SGD, f reaches minimum validation loss  **l'** at iteration **j'** with test accuracy **a'**. The lottery ticket hypothesis predicts that there exists an **m** for which **j' <= j** (similar training time), **a' >= a** (similar accuracy) and **||m|| << |w|** (fewer parameters). 
* When their parameters are randomly reinitialized, winning tickets no longer match the performance of the original network which shows that these smaller networks do not train effectively unless they are appropriately initialized.
* Steps:
  - Randomly initialize a neural network f(x; w0).
  - Train the network for j iterations, arriving at parameters wj.
  - Prune p% of the parameters in wj, creating a mask m.
  - Reset the remaining parameters to their values in w0, creating the winning ticket.

* They do iterative pruning, which repeatedly trains, prunes, and resets the network over n rounds; each round prunes p^(1/n) % of the weights that survive the previous round.