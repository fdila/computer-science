% Advanced Machine Learning, 2021/2022
% Federica Di Lauro
%

# Deep learning

Deep learning -> NN with several layers of nodes.

Deep learning is inspired by our brains.

## Feed Forward Neural Networks

Alghoritms for training multilayer networks are complex.

**Weight learning**: dumb.
If $f(x)$ is non-linear in theory we only need a single hidden layer.

Multi-layer networks recognize different "levels" of features depending on the layer "level".

A way to train multi-layer NNs is to train first the first layer, then the second, and so on..

Each layer (apart from the output layer) is trained to be an auto-encoder.

The auto-encoder wants to encode the stuff, ignoring the noise.

- Feed Forward NN: no loops, arrows go only in next layer. Usually they are fully connected, which makes them prone to overfitting

- Recurrent NN: loops on the nodes, the looping ensures that sequential information is captured in the input data.

- Convolutional NN: hierarcal pattern in data, assemble complex patterns using smaller and simpler patterns. Very effective in image recognition. Not all layers in the neurons are connected to next layer.




