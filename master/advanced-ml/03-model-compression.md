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

## Low rank decomposition

Most weights are in the fully connected layers.
FC layers are implemented by a matrix multiplication, the weights which connect a layer with $N$ units to a layer with $M$ units is a $N \times M$ matrix.

We can decompose this matrix with the SVD decomposition. We then keep only the singular values with largest magnitude and reconstruct the $W$ matrix.

The resulting matrix will have a lower rank than the original one.

## Knowledge distillation

## Quantization

## Low resource and efficient architectures