# Attention Residuals

{% embed url="https://arxiv.org/abs/2603.15031" %}

Notes:

* Problem: Amnesia&#x20;
  * The original motivation for residual connections was to propgate gradients
    * Vanishing gradient problem
  * "This uniform aggregation causes uncontrolled hidden-state growth with depth, progressively diluting each layer's contribution."
* Solution: KQV based residuals
  * "Softmax attention over preceding\
    layer outputs, allowing each layer to selectively aggregate earlier representations with learned, input  dependent weights."
* Physical Constraints
  * LLMs are often trained on parrallel blocks of GPUs, where the output of one block of layers is fed into the next block
  * If all residuals must be attended to, there is massive increases in compute time and network communication that makes this highly inefficient
  * Solution: Block AttnRes
    * Partition layers into blocks and perform block level attention, rather than the entire network of potentially thousands of layers
    * Slight tradeoff in model performance, big decrease in training cost
