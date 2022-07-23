# BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding

Devlin, Jacob, et al. "Bert: Pre-training of deep bidirectional transformers for language understanding." arXiv preprint arXiv:1810.04805 (2018).

## What

A model to generate bidirectional encoder representations.  

## Why

Previous models such as OpenAI GPT only attend to previous tokens. Such restrictions are sub-optimal for sentence-level tasks,
and could be very harmful when applying fine-tuning based approaches to token-level tasks such as question answering, where it is crucial to incorporate context from both directions.

## How

Randomly masks some of the tokens from the input, and the objective is to predict the original vocabulary id of the masked word based only on its context.

## Notes

* **B**idirectional **E**ncoder **R**epresentations from **T**ransformers.
* Jointly conditions on both left and right context in all layers
* Standard conditional language models can only be trained left-to-right or right-to-left, since bidirectional conditioning would allow each word to indirectly “see itself”, and the model could trivially predict the target word in a multi-layered context. 
* In order to train a deep bidirectional representation, they mask some percentage of the input tokens at random, and then predict those masked tokens.