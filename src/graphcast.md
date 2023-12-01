# GraphCast

Graphcast is a graph neural network architecture with an encoder-decoder
configuration. The graph neural network is used to encode unstructured input data into a graph
representation. As opposed to, for instance, convolutional layers where neighbouring information
is encoded in a structured grid, graph layers use message passing between nodes to capture the
relationships between different parts of the input data. This allows for the encoding of different kind
of information, not necessarily restricted to a grid configuration.

![GraphCast](../imgs/graphcast2.png)

One important hyperparamter to be set in this kind of architectures is the number of hops the
messages containing neighbouring information are allowed to travel. This is crucial for the model to
learn from the correct amount of knowledge, and allows for reducing the computational complexity of
the model, as the number of hops is directly related to the time required for the model to train.

![GraphCast](../imgs/graphcast1.png)
