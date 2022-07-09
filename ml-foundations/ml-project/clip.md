---
description: Contrastive Language-Image Pre-training
---

# CLIP

#### Overview and Context

CLIP is used to learn semantic meaning from natural language, which can be used for things like Dalle e 2.  Rather than learning to predict a caption based on images, it instead learns to gauge how related an image is to a caption. In this way, it captures a more abstract view of complex relationships between natural language, semantics, and visual information. Because it doesn't predict, this model is instead known as a contrastive technique, hence the name.

#### Training

Training involves a few steps, the training data is the captions and respective images:

1. All captions and images are encoded into an m-dimensional vector
   1. WebImageText dataset is the actual training data
   2. The image encoder is [https://arxiv.org/abs/2010.11929](https://arxiv.org/abs/2010.11929)
   3. The text encoder is [https://arxiv.org/abs/1706.03762](https://arxiv.org/abs/1706.03762)
2. The cosine similarity between image and caption is calculated
   1. For reference, cosine similarity is the inner product of two vectors, weighted by the product of the magnitudes. It captures the angle between two vectors, which is a representation of similarity.
3. The goal is to maximize the similarity between N correct pairs while minimizing the similarity between the other N^2 - N pairs.

Additional: The algorithm works by encoding all pairs, then training to increase similarity between correct pairs, and finally decreasing similarity between incorrect pairs. As each pair's result is independent of other results, this process can be parallelized, making it very efficient with enough compute.

#### Why CLIP

The beauty of CLIP is that it attempts to capture the ultimate goal of AI: to imitate human intelligence and the ability to understand meaning rather than memorizing. CLIP doesn't just try to predict a caption from an image based on recognition of certain features like edge detectors and line detectors, it actually attempts to assign visual meaning to natural language, much like the human brain. We have complex understanding of the world that requires the ability to understand meaning rather than memorizing visual features. Of course, recognizing visual features is also crucial, but the idea of capturing the "platonic ideal" is what allows our understanding and interpretability. It really is a question of metaphysics here and the idea of "knowing" and capturing what "is".

From [https://www.assemblyai.com/blog/how-dall-e-2-actually-works/](https://www.assemblyai.com/blog/how-dall-e-2-actually-works/)

> This result is significant because it shows that CLIP learns the **semantic link between text descriptions of objects and their corresponding visual manifestations**. Rather than relying on specific details of image instances, like the yellow color of bananas, to identify them as a convolutional ResNet might, CLIP learns the semantic "Platonic ideal" of what a banana _"is"_, allowing it to better identify sketches of bananas. Understanding the fact that textual descriptions and visual features can map to the same "Platonic ideal" is crucial for text-conditional image generation, and this is why CLIP is so important to the DALL-E 2 paradigm.
