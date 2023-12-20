# GNN Transformers

## Introduction 

A graph is a kind of data structure, which is composed of nodes (objects) and edges (relationships).

Most of the current GNNs are based on the message passing paradigm, which is a generalization of the convolutional neural networks (CNNs) to non-Euclidean domains.

Often GNNs suffer from the following problems:
- **Over-smoothing**: the information from the nodes is averaged out, and the model cannot distinguish between nodes that are far away from each other.
- **Over-squashing**: due to the exponential computation with the increase in model depth.

## Use of GNNs in Transformers

There have been developed three main ways to use GNNs in Transformers:
- Auxiliary Modules: GNNs are used to inject auxiliary information to improve the performance of the Transformer.
- Improve Positional Embedding with Graph: compress the graph structure into positional embedding vectors, and input them to the Vanilla Transformer.
- Improve attention matrix from graph: inject graph priors into the attention computation via graph bias terms. 

These type of modifications tend to yield improved performance both on node level and graph leevel tasks, more efficient training and inference, and better generalization. This being said different group models enjoy different benefits.

Graph building blocks can be used on top of existing attention mechanisms, can be alternated with self-attention layers, or can be used in conjunction (concatenated) with existing transformer blocks. 

## Some Architectures

- **GraphTrans**: adds a transformer sub-networkon top of a standard GNN layer. It performs as a specialized architecture to learn local representation, while the transformer sub-network learns global representation of pairwise node interactions.
- **Grover**: uses two GTransformers to learn node and edge representations, respectively. The node representations are then used to update the edge representations, and vice versa. The inputs are first passed to a GNN which is trained to extract vectors as query, key and value. This layer is then followed by a self-attention layer.
- **GraphiT**: adopts a Graph Convolutional Kernel Network layer to produce a stucture aware embedding of the graph. The output of this layer is then passed to a self-attention layer.
- **Mesh Graphormer**: stacks Graph residual blocks on a multi-head self-attention layer. The graph residual block is composed of a graph attention layer and a graph feed-forward layer. It improves the local interactions using a graph convolutional layer in each transformer block.
- **GraphBERT**: uses graph residual terms in each attention layer. It concatenates the graph residual terms with the original attention matrix, and then applies a linear transformation to the concatenated matrix.

## Positional Embeddings

It is also possible to compress the grqph structure into positional embedding vectors, and input them to the Vanilla Transformer. Some approaches adopt Laplacian eigenvectors as positional embeddings, while others use svd vector of adjacent matrices as positional embeddings. 