---
description: Cool openAI thing
---

# Dalle e 2

### Overview

{% embed url="https://www.assemblyai.com/blog/how-dall-e-2-actually-works/" %}
good article
{% endembed %}

#### Text to Image pre-training

In this stage the goal is to translate semantics to visual representation. Instead of a predictive model that predicts what caption a given image has, it actually just learns how related a caption and image are. This is why it is called a contrastive model rather than predictive. Therefore, the model learns a more abstract relationship between semantics and visual representation, allowing it derive meaning from natural language which can be translated to visual information. More on this and how it actually is trained here:

{% content-ref url="clip.md" %}
[clip.md](clip.md)
{% endcontent-ref %}

#### Image generation

CLIP is useful for deriving semantics and finding similarity between image and text, however we also need to be able to take a caption and generate an image. To better understand this process, it is necessary to know how diffusion works. More on that here:

{% content-ref url="../diffusion-in-ml.md" %}
[diffusion-in-ml.md](../diffusion-in-ml.md)
{% endcontent-ref %}

#### Training
