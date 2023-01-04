# Generative Models

Description

Generative tasks are tasks with the goal of creating and new example of X. We have a learned system that takes in some randomness and context, and it outputs an example of X. X could be language, images, etc. There are various uses of generative models, such as creating new training data, "encrypting" sensitive data (called "data laundering"), and also just for the purpose of generation (Dall-e, GPT, etc.).

#### Autoregressive Generation

The idea behind autoregressive generation is to try to sample some random vector x from a known distribution. However, we are able to do it using CDFs and a uniform random vector u. For the exact steps, see page 2 of my lecture note titles "Generation Models 2" below.

#### Other models

The naive idea is to just use an autoencoder and add randomness to the latent vector between the encoder and decoder. This has worked well for small amounts of randomness, this is known as a denoising autoencoder. These can be very useful in making encoders more robust and in avoiding "learning the identity" (more on this elsewhere). However, for generation tasks, we need to input too much randomness, which leads this method to be pretty bad. We see when we take an autoencoder and add a classification head, adding too much noise leads our output to just look like noise.&#x20;

#### GAN approach

I may end up writing a whole note on this, but I'll summarize here. Essentially, the idea behind generative adversarial networks (GANs) is to train both a generator and a classifier. This classifier, known as a discriminator, is tasked with classifying if input is "real or fake". The real data is just examples from the dataset, and the fake data is the output from the generator. The training process is typically to freeze the generator, then optimize the descriminator with SGD. It's essentially just a classification problem, so we can our standard settings like cross-entropy loss and SGD. Next, we freeze the discriminator and optimize the generator with similar gradient based optimization techniques. Overall, it looks like the minimax problem below. Below also is pseudocode for training.

![](<../.gitbook/assets/image (7).png>)

Some issues with Gans:

* GAN training is hard -> can be unstable and it tends to osciallate
* If the discriminator is too good, we have tiny gradients
* Mode Collapse: when generation lacks sufficient diversity

#### Diffustion Approach

{% content-ref url="diffusion-in-ml.md" %}
[diffusion-in-ml.md](diffusion-in-ml.md)
{% endcontent-ref %}

### Course Notes

My course notes about generative models from CS 182:

{% content-ref url="../lecture-notes/cs-182/generative-models-1.md" %}
[generative-models-1.md](../lecture-notes/cs-182/generative-models-1.md)
{% endcontent-ref %}

{% content-ref url="../lecture-notes/cs-182/generative-models-2.md" %}
[generative-models-2.md](../lecture-notes/cs-182/generative-models-2.md)
{% endcontent-ref %}

{% content-ref url="../lecture-notes/cs-182/generative-models-3.md" %}
[generative-models-3.md](../lecture-notes/cs-182/generative-models-3.md)
{% endcontent-ref %}
