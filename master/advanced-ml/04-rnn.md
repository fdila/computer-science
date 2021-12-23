
# RNNs

RNNs are a family if NN for processing sequential data. They process a sequence of values.

Parameters are shared across time.

Most relevant architectures:

- RNNs that produce an output at each time step and have recurrent connections between units
- RNNs that produce an output at each time step and have recurrent connections only from the output at one time step to the hidden units at the next time step.
- RNNs with recurrent connections between hidden units, that analyze an entire sequence and then produce a single output

The gradient at each time step depends on both the calculation of the current time step and the calculation of the previous time step.
The training algorithm for RNN is called **Backpropagation Through Time (BPTT)**
We need to backpropagate the gradients from the output through the network all the way back to t = 0.

RNNs suffer from vanishing gradients problem because we multiply many small numbers togheter, the errors due to further back time step have smaller and smaller gradients: this introduce a bias such that parameters capture only short-term dependencies.

Solutions:

1. Choosing an appropriate activation function
2. Parameters initialization: initialize weights to identity matrix and biases to 0
3. Use a more complex recurrent unit with gates to control what information passes through

**Gated RNNs**: both LSTM (Long Short-Term Memory) or Gated Recurrent Units (GRU)
There are paths that have derivatives that neither vanish nor .
They use connection weights that may change at every time step.

## LSTM

Organized in cells, there are several operations in each cell.

3 different tipe of Operation Gates:

- Forget Gate
- Input Gate
- Output Gate

**Cell state**: mantains a vector $C_t$ that has the same dimensionality as the hidden state $h_t$
Information can be added or deleted from this state vector via the forget gate or the input gate.

**Forget Gate**: sigmoid layer that takes the previous hidden state and the current input, concatenates them and applies a linear transformation followed by a sigmoid.

If $f^{(t)} = 0$ then the previous internal state is completely forgotten, if $f^{(t)} = 1$ the previous internal state will be passed through unalterated.

**Input Gate**: determines which entries in the cell state to update by computing the sigmoid output.
Then determines what amount to add/subtract from this entries by computing a tanh output function of the input and the hidden state.

Cell state is updated by using component-wise vector multiplication to forget and vector addition to include new information.

**Output Gate**: hidden state is updated based on a filtered version of the cell state, scaled to [-1,1] using tanh.
Output gate computes a sigmoid function of the input and the previous state to determine which elements of the cell state to output.

Application architectures:

- One to many (image captioning)
- Many to one (Video activity recognition, text classification)
- Many to many(video captioning, machine translation, language modelling)

## GRU

- Alternative to LSTM that uses fewer gates
- Combines forget and input gates into "update" gate
- Eliminates cell state vector
- Significant less parameters than LSTM and trains faster

