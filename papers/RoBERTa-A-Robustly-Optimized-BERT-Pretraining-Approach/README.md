# RoBERTa: A Robustly Optimized BERT Pretraining Approach

Liu, Yinhan, et al. "Roberta: A robustly optimized bert pretraining approach." arXiv preprint arXiv:1907.11692 (2019).

## What

They claim that BERT is undertrained and provide a new pretraining approach.

## Why

To have more fair comparisons?

## How

By providing a careful evaluation of the effects of hyperparmeter tuning and training set size.

## Notes

* (1) Training the model longer, with bigger batches, over more data; 
* (2) Removing the next sentence prediction objective 
* (3) Training on longer sequences
* (4) Dynamically changing the masking pattern applied to the training data
* Two training objectives:
  * Masked language modeling
  * Next sentence prediction