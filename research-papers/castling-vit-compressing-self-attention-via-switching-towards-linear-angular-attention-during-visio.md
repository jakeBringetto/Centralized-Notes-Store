---
description: Big mathington vibes
---

# Castling-ViT: Compressing Self-Attention via Switching Towards Linear-Angular Attention During Visio

{% embed url="https://arxiv.org/pdf/2211.10526.pdf" %}
&#x20;
{% endembed %}

### Summary

This paper was inspired by the appearance of vision transformers (ViT), which was a strategy for using out of the box transformer architecture to do computer vision tasks such as image classification. More on that can be read here:

{% content-ref url="an-image-is-worth-16x16-words-transformers-for-image-recognition-at-scale.md" %}
[an-image-is-worth-16x16-words-transformers-for-image-recognition-at-scale.md](an-image-is-worth-16x16-words-transformers-for-image-recognition-at-scale.md)
{% endcontent-ref %}

In this paper the authors try to tack a few problems, mostly focusing on the efficiency of vision transformers during inference. The industry standard decribed both in papers like "All You Need is Attention" and the ViT paper linked above use soft-max based attention functions. These, as you know, are quadratic with respect to input token length and linear with respect to the dimension, which presents itself as a problem when N >> D. The goal of this paper is to create an attention approach that is linear with respect to N and instead quadratic in D. Now, obvsiously this has been done before and is one of the large reasons for using kernalized versions of soft-max attention, including the polynomial kernal and the guassian approximation (RBF kernal).
