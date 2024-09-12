# Test time training (TTT)

> [Paper]()

- Transformers: O(N^2) complexity due to self-attention. 
- Mamba and advanced RNNs: O(N) complexity, but latent space is fixed, still subject to catastrophic forgetting

## TTT methods

New class of sequence modelling layers where the hidden state is a model, and the update rule is a step of self-supervised learning.
The process is updating the hidden state even during the test time. 

Self attention has hidden state growing linearly with the sequence length (cost is per token), while TTT has a fixed size hidden state.

TTT compresses the historical context into a hiddden state St, making the context an unlabelled dataset.
