# Convolutional Neural Networks

In the convolutional layers the weights are arranged in 3 dimensions.

The connectivity between the input and the convolutional filter is: 

- local in space (small filter kernel which slides on the full image)
- full in depth (all 3 depth channels)

Apart from the convolutional layer in CNNs we also have other special layers:

- Spatial pooling
- Local response normalization

These layers are useful to:

- reduce computational burden
- Increase invariance
- Ease the optimization

## Specific layers for CNNs

### Linear convolution

- **Input** $x = H \times W \times K$
- **Filter bank** $F = H' \times W' \times K \times Q$
- **Output** $(H - H' + 1) \times (W - W' + 1) \times Q$

$$
y_{ijq} = y_q + \sum_{u=0}^{H-1} \sum_{v=0}^{W-1} \sum_{k=1}^{K-1} x_{u+i, v+j, k} F_{u,v,k,q}
$$

[Convolution GIF](https://upload.wikimedia.org/wikipedia/commons/1/19/2D_Convolution_Animation.gif)

We can also apply the filter not by sliding the kernel pixel-by-pixel.
We can slide the kernel by $s$ pixels, this is called the **stride**.

Also notice that by applying the convolution the width of the representation shrinks by one pixel less than the kernel width
at each layer. To avoid this we can use **padding** on the input so that the output size remains the same.

### Spatial pooling

Pooling computes the average/max of the features in a neighbourhood.
It is applied channel by channel.
It is so a form of subsampling which reduces the dimensionality of our 2D features.

- Aggregates to achieve translation invariance (gain robustness to the exact spacial location of features)
- Subsampling reduces spatial scale and computation

### Local Response Normalization

Contrast normalization.

- Improves invariance
- Improves optimization
- Improves sparsity

Within channel:

- operates indipendently on different features channels
- rescales each input feature basing on local neighborhood

Across channels:

- Operates independelty at each spatial location and groups of channels
- Normalizes groups G(k) of feature channels
- Groups are usually defined in a sliding window manner

_Many types of normalization layers have been proposed for use in ConvNet architectures, sometimes with the intentions of implementing inhibition schemes observed in the biological brain. However, these layers have recently fallen out of favor because in practice their contribution has been shown to be minimal, if any._


## Data preprocessing

**Local mean subtraction**: subtract the mean from the original data

$$
X = X - \mu
$$

**Normalization**: scale original data to a specific range

$$
X = \frac{X - \mu}{\sigma}
$$

## Training CNNs

Regularization:

- Weight decay
- Dropout: usually not used for convolutional layers
- Data augmentation: flipping, cropping, color casting, geometric distortion

## CNN Architectures

### LeNet (LeNet-5)
First CNN (1998)

### AlexNet
First CNN that won ImageNet challange.

Large conv filter in the beginning.

### VGG

Family of NNs.

Just 3x3 conv filters.

A stack of 3x3 conv filters has the same receptive field as one 7x7.
It makes the CNN deeper, with more non-linearities and fewer parameters.

### GoogLeNet (Inception)

Design a good local network topology (network within a network) and then stack multiple times this blocks

Use 1x1 conv layers as **bottlenecks** to reduce feature depth

We use 9 inception modules stacked on top of each other.
2 auxiliary classifiers to inject additional gradients at lower layers to avoid the vanishing gradient problem.
  
### ResNet

Deeper model usually perform better but we can't keep adding layers because deeper models are harder to optimize (e.g. the vanishing gradient problem).

The resnet solution is to use network layers to fit a residual mapping instead of directly trying to fit a desired underlying mapping.

So there are some connection between some layer and a deeper layer so that the gradient can "skip"

- Stack **residual blocks**
- Every residual block has two 3x3 conv layers
- For deeper nets use bottleneck layers to improve efficiency
- Periodically double the number of filters and downsample using a stride of 2 (using a conv layer with stride 2 halves the dimension, using a maxpool layer would be computationally inefficient)
- A lot of small conv layers with 2 final fully connected layers

## Transfer learning

It's common to use a pretrained CNN which has been trained on a very large dataset and then use the CNN either for fine tuning or as a fixed feature extractor for the task of interest.

_How to decide which type of TL to perform?_

- New dataset is small and similar to the original dataset: train a linear classifer on CNN features from higher layers

- New dataset is large and similar to the original dataset: fine tune the CNN

- New dataset is small but very different from the original dataset: train a linear classifier on CNN features from lower layers

- New dataset is large and very different from original dataset: train CNN from scratch or fine tune it


