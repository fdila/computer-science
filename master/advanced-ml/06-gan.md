# Generative Adversarial Networks (GANs)

Generation (from scratch): learn to sample from the distribution represented by the training set.

Conditional generation: generation of image belonging to a specific class

Image-to-image translation: starting from an image and output an image.

**Designin a network for generative tasks:**

1. We need an architecture that can generate an image
2. We need to design the right loss function

**Upsampling in a deep network:** it's a transposed convolution.

With GANs we train 2 networks with opposing objectives:

- Generator $G(x)$: learns to generate samples
- Discriminator $D(x)$: learns to distinguish between generated and real samples.

**GAN objective**

The discriminator should output the probability that the sample x is real: we want it to be close to 1 for real data and 0 for fake.

Training the generator and discriminator jointly in a _minmax game_.

Theoretically, if we assume:

- unlimited capacity for generator and discriminator
- unlimited training data
- at each step the models are allowed to reach the optimimun

the distribuition of the generated data would converge to the distribution of the real data.

**GAN training**

Alternate between:

- Gradient ascent on discriminator
- Gradient decent on generator

**GAN training algotithm**

- Update discriminator
    - repeat for $k$ steps
        - sample mini-batch of noise samples and mini-batch of real samles
        - update parameters of D by SGD
- Update generator
    - sample minibatch of noise samples
    - update parameters of G by SGD

Repeat until happy

## Problems

- Stability
    - Parameters can oscilate or diverge, generator loss does not correlate with sample quality
    - Behavior is very sensitive to hyper-parameter selection

- Mode collapse:
    - Generator ends up modelling only a small subset of the training data

## Training tips and tricks

- Make sure discriminator provides good gradients to the generator even when it can confidently reject all generator samples:
    - use non- saturating generator loss
    - smooth discriminator for real data, eg label smoothing
- Use class labels in the discriminator if available:
    - for a dataset with $C$ classes have the discriminator perform
    $C+1$ class classification, where the $+1$ is the "fake" label

## Evaluating GANs

- Turing test: using real humans to judge if the image is fake
- Inception score: use an architecture that has been trainied to recognize real objects. Measure the activations inside the network. Usually InceptionNet is used.

## Examples

**DCGAN**: propose principles for designing convolutional architectures for GANs.
Reduce depth resolution to increase the spatial resolution.
Uses the transposed convolution.

**Wasserstein GAN**: better gradients, more stable training. Objective function is more meaningfully related to quality of generator output.



