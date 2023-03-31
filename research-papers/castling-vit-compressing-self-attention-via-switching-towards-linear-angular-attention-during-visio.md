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

We begin by recalling that similarity between vectors can be captured with the angle between two vectors using trigonometry:

$$
\theta(x, y) = \arccos(\dfrac{x^Ty}{\|x\|\|y\|})
$$

Using this, we can define a new similarity function:

$$
sim(q, k) = 1 - \dfrac{1}{\pi}\theta(q, k)
$$

Now we can explore some of the properties of this new feature space created by the implicit kernel. We'll see some rather interesting observations when we delve deeper into this.

Let's first look at the magnitude of a vector projected into the implicit feature space:

$$
\|\phi(x)\|^2 = \phi(x)^T\phi(x) = sim(x, x) = 1 - \dfrac{1}{\pi}\cdot0
=1
$$

This is an interesting result because we see that the magnitude of a vector in the implicit feature space is always 1 - meaning that all points lie on a sphere of radius 1.

Next, let's consider the euclidean distance between two vectors in feature space:



$$
\|\phi(x) - \phi(y)\|^2 = 1 + 1 - 2\cdot\phi(x)^T\phi(y)
=2(1 - sim(x, y))
=\dfrac{2}{\pi}\theta(x, y)
$$

We observe here that the euclidean distance in feature space is positively correlated with the spectral angle between the two vectors. That is, increasing the spectral angle between two vectors leads to an increase in the euclidean distance in feature space. Thus, the max distance occurs when the angles are at 180 degrees with distance 2.

Now we work towards a linear-angular attention method using the ideas above. The following equation can be derived using trigonometry identities and the Taylor expansion of arcsin:

$$
sim(q, k)= \dfrac{1}{2} + \dfrac{1}{\pi}\cdot(\dfrac{q^Tk}{\|q\|\|k\|}) + \dfrac{1}{\pi}\sum_{i=1}^{\infty} \dfrac{(2i)!}{2^{2i}(i!)^2(2i+1)}(\dfrac{q^Tk}{\|q\|\|k\|})^{2i+1}
$$

The above equation has the first terms that can be computed in linear time, but the last terms are much more complex. We solve this problem by approximating these terms with a Matrix M. This leads us to the final equation, which is:

$$
V' = Sim(Q, K) \cdot V \approx 1/2 \cdot V + \dfrac{1}{\pi}Q \cdot(K^T \cdot V) + M_{DW} \cdot V + M_{SparseAtt} \cdot V
$$

Note that M\_DW approximates the high order terms from above using a depthwise convolution. M\_SparseAtt is another matrix learned in training that is very sparse. In fact, most of the values tend to be 0, more on that can be found in the paper.

Another thing to note is that above we don't see the normalization we above. This is still done using a normalization kernel that works very efficiently, however it is left out for simplicity.&#x20;

The main take-away from the above equation is that we can compute all terms in linear time with respect to the token length N and quadratic time with respect to the dimension D.

#### Sparse Attention&#x20;

During inference the authors only use spectral angle attention to capture similarity, however they keep soft-max attention during training. They do this with the sparse matrix seen above. Essentially, it is standard soft-max attention but we only pass values if they are bigger than some threshold we set as a hyper-parameter. The effect this has is that it captures some of the higher order terms that we may miss in spectral angle attention. Additionally, making it sparse has the effect of only selecting strong local features. So the idea is that we add terms we missed, but only if they are strong features. Then in inference we remove the soft-max architecture and only use the   spectral angle attention.

#### Architecture

![](<../.gitbook/assets/image (5).png>)





