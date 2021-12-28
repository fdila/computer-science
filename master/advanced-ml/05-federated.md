# Federated Learning

Federated Learning (FL) aims to collaboratively train a ML model while keeping the data
decentralized

We don't centralize the data because:

- Sending the data could be too costly
- Data may be considered too sensitive

We can't train separete model for each party:

- The local dataset may be too small
- The local dataset may be biased

**Differences with distributed learning**

In distributed learning data is centrally stored and then distributed across workers to train the model faster.
In federated learning data is naturally distributed and generated locally.

**Cross-device vs cross-silo**

- Cross-Device FL:
    - Massive number of parties (up to 10^10)
    - Small dataset per party
    - Limited availabilty and reliability
    - Some parties may be malicious
- Cross-silo FL:
    - 2-100 parties
    - Medium to large dataset per party
    - Reliable parties, almost always available
    - Parties are typically honest

**Server orchestrated vs fully decentralized**

- Server orchestrated FL:
    - Server-client communication
    - Global coordination, global aggregation
    - Server is a single point of failure and may become a bottleneck.
- Fully decentralized FL:
    - Device-to-device communication
    - No global coordination, local aggregation
    - Naturally scales to a large number of devices

## FedAVG

1. The server initializes the model and sends it to the clients.
2. Each client updates the model indipendently and sends the updated model to the server for $L$ steps.
3. The server takes all the model and for each parameter it averages the values.
4. The server send back the updated model to the clients. GOTO 2

For $L = 1$ it is equivalento do classic parallel SGD: updates are aggregated and the model synchronized at each step.

For $L > 1$ multiple local SGD steps before communicating. It allows to reduce the number of communications which is often the bottleneck in FL.
It empirically achieves better generalization than parallel SGD with large mini-batch.

Convergence to the optimal model can be guaranteed for indipendet and identically distributed data, but issues aries in strongly non-i.i.d. case.

## FL of personalized models

Learning from non-i.i.d data is difficult and slow because each party wants the model to go in a particular direction.

If data distributions are very different learning a model which performs well for all parties may require a very large number of parameters.

Another direction to deal with non-i.i.d. data is to lift the requirement that the learned model should be the same for all parties

Instead, we can allow each party to learn a personalized model but design the objective so as to enforce some kind of collaboration.

**Personalized models from a meta model**:

1. regularize personalized models to their mean
2. inspired by meta-learning: learn a global model that can be adapted to each party


