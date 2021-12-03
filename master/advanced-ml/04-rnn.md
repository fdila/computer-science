# Recurrent and Recursive neural networks

RNNs are a family if NN for processing sequential data. They process a sequence of values.

Parameters are shared across time.

RNNs suffer from vanishing gradients problem. 
Solutions:

1. Choosing an appropriate activation function
2.
3. Use a more complex recurrent unit with gates to control what information passes through

**Gated RNNs**: both LSTM (Long Short-term memory) or Gated Recurrent Units (GRU)
There are paths that have derivatives that neither vanish nor explode
They use weights that change.

