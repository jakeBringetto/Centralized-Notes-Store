---
description: Transformer with Fine- and Coarse-Grained Attention for Music Generation
---

# Museformer

{% embed url="https://arxiv.org/pdf/2210.10349" %}

### Notes:

* Challenges of music generation
  * Long sequence modeling&#x20;
  * Music structure modeling
* Transformer with fine and coarse grain attention
  * Correlations of structure related bars via fine grain
  * Concentrated information of other bars via coarse grain
* Structure related bars are selected based on statistics from human made music
* FC-attention to replace standard softmax attention
  * Local fine grain attention on selected bars
  * Course grain attention using a summarization token
* First summarize local info via a summarization step, then aggregate coarse and fine grain information via an aggregation step
* Summarization:

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

* Aggregation:

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

* Merits:
  * Receptive field of fine grain attention comply with musical structure
  * Coarse grain attention can preserve information needed for better music
    * Normal sparse attention drops a lot of information
  * Combining fine and coarse grain attention keeps quality while preserving computation efficiency (effectively linear attention in inference)
* Evaluation metrics:
  * Perplexity
  * Similarity error
  * Musicality
  * Long/short term structure
  * Preference score (rated by humans with varying musical expertise)
