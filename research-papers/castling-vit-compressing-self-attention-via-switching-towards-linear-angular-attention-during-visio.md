---
description: Big mathington vibes
---

# Castling-ViT: Compressing Self-Attention via Switching Towards Linear-Angular Attention During Visio

{% embed url="https://arxiv.org/pdf/2211.10526.pdf" %}
&#x20;
{% endembed %}

### Overview

This paper was inspired by the appearance of vision transformers (ViT), which was a strategy for using out of the box transformer architecture to do computer vision tasks such as image classification. More on that can be read here:

{% content-ref url="an-image-is-worth-16x16-words-transformers-for-image-recognition-at-scale.md" %}
[an-image-is-worth-16x16-words-transformers-for-image-recognition-at-scale.md](an-image-is-worth-16x16-words-transformers-for-image-recognition-at-scale.md)
{% endcontent-ref %}

In this paper the authors try to tackle a few problems, mostly focusing on the efficiency of vision transformers during inference. The industry standard described both in papers like "All You Need is Attention" and the ViT paper linked above use soft-max based attention functions. These, as you know, are quadratic with respect to input token length and linear with respect to the dimension, which presents itself as a problem when N >> D. The goal of this paper is to create an attention approach that is linear with respect to N and instead quadratic in D. Now, obviously this has been done before and is one of the large reasons for using kernelized versions of soft-max attention, including the polynomial kernel and the gaussian approximation (RBF kernel). However, it's been observed that the performance of these kernels is not as good as soft-max attention. This paper introduces another method of capturing "distance" by utilizing the spectral angle between keys and queries. It's found in the paper that using their process leads to results comparable to soft-max based methods while also maintaining linear attention w.r.t. token length.

### Methodology

Their are two main strategies that I will discuss that are deployed by the authors of this paper. The first is spectral angle attention and the other is the sparse attention matrix which I'll explain in more detail later.

#### Spectral Angle Attention

Note that this section is taken from my cs182 project that delves deeply into this spectral angle based attention. More on that found here:

We begin by recalling that similarity between vectors can be captured with the angle between two vectors using trigonometry.

