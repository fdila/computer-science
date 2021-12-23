# Model Compression

Key points:

- Smaller size
- Accuracy: no loss of accuracy of improved accuracy
- Speedup: make inference faster

Main approaches:

- Weight sharing
- Network pruning
- Low rank matrix and tensor decomposition
- Knowledge distillation
- Quantization

- Low resource and efficient architectures (not really a compression method, we begin constructing the NN with efficienty in mind)

## Weight sharing

- Share weights between layers or structures within layers (e.g. filters in CNNs)
- Carried out prior to training
- Reduces network size and avoids sparsity

## Network pruning

It's the most commonly used technique to reduce the number of parameters in a pretrained NN. It can lead to reduction of storage and model runtime.
Performance is usually mantained by retraining the pruned network. Iterative weight pruning prunes while retraining untile the desired network size and/or accuracy tradeoff is met.

Categories of pruning techniques:

- Magnitude-based pruning: the weights with the lowest absolute value of the weights are removed based ona set treshold or percentage, layer-wise or globally.
- Methods that penalize the objective with a regularization term to force the model to learn a network with smaller weights, and then prune the smallest weights
- Methods that compute the sensistivity of the loss function when weights are removed and using this as a criterion for removing weights that result in the smallest change in loss. (Optimal Brain Damage)
- Search-base approaches (e.g. particle filter, evolutionary algotithms, reinforcement learning) that seek to learn or adapt a set of weights to links or paths within the neural network and keep those that are salient for the task.

**Structured vs unstructured pruning:**

- structured aims to preserve the network density for computational efficiency by removing groups of weights
- unstructured is unconstrained to which weights or activations are removed but the sparsity means that the dimensionality of layers doesn't change.

Sparsity in unstructured pruning provides good performance at the expense of slower computation: the weights must be memorized in sparce matrixes but sparse matrix multiplication is typically slower than dense multiplication.

Group sparsity regularization enforce a subset of weight groupings, such as filters in CNNs, to be close to zero.

## Low rank decomposition

Most weights are in the fully connected layers.
FC layers are implemented by a matrix multiplication, the weights which connect a layer with $N$ units to a layer with $M$ units is a $N \times M$ matrix.

We can decompose this matrix with the SVD decomposition. We then keep only the singular values with largest magnitude and reconstruct the $W$ matrix.

The resulting matrix will have a lower rank than the original one.

## Knowledge distillation

Knowledge distillation involves learning a smaller network from a large network using supervision from the larger network and minimizing the entropy, distance or divergence between their probabilistic estimates.

## Quantization

Quantization is the process of representing values with a reduced number of bits. In neural networks, this corresponds to weights, activations and gradient values.

To speed up training, faster inference and reduce bandwidth memory requirements, ongoing research has focused on training and performing inference with lowerprecision networks using integer precision (IP) as low as INT-8, INT-4, INT-2 or 1 bit representations.

## Low resource and efficient architectures

### MobileNet

Compression of CNNs for embedded and mobile vision application using depth-wise separable convolutions (DSC) and use two hyperparameters that tradeoff latency and accuracy

DCSs factorize a standard convolution into a depthwise convolution and 1x1 pointwise convolution.

Each input channel is passed through a DSC filter followed by a pointwise 1x1 convolution that combines the outputs of the DSC.

Unlike standard convolutions, DSCs split the convolution into two steps, first filtering then combining outputs of each DSC filter, which is why this is referred to as a factorization approach.

### SqueezeNet

Reduce the network architecture by reducing 3x3 filters to 1x1 filters
(squeeze layer)

### ShuffleNet

ShuffleNet uses pointwise group convolutions (i.e using a different set of convolution filter groups on the same input features, this allows for model parallelization) and channel shuffles (randomly shuffling helps information flow across feature channels) to reduce compute while maintaining accuracy. 

### DenseNet

DenseNets address gradient vanishing connecting the feature maps of the previous layer to the inputs of the next layer, similar to ResNet skip connections. This reusing of features mean the network efficient with its use of parameters.
