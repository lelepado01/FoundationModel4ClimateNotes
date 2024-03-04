# Multi-scaled stacked ViT

Development of an efficient ViT: 
- Adds a layer normalization after the patch embedding operation; 
- Global and Local token differentiation; 
- Self-attention mechanism is replaced with efficient multi-scaled self-attention mechanism; 
- Positional embedding 1-D is replaced with 2-D positional embedding or absolute positional bias. 

## Multi-scaled self-attention mechanism

Uses a local attention plus global memory approach. Define the **n_g** global tokens that are allowed to attend to to all tokens, and the **n_l** local tokens that are allowed to attend to the tokens in their local 2D window area and only the global tokens. 

**Relative positional bias**: add a bias matrix to each head when capturing the attention score (makes the transfomer translation invariant). 

Theoretical complexity: **n_g** and **n_l** are global and local token numbers, the memory complexity is \\( O( n_g(n_g + n_l) + n_l w^2 ) \\). 

## Comparisons

**Linformer**: projects \\( **n_l** \times d \\) dimensional keys and values to \\( K \times d \\) with an additional linear projection layer, where \\( K << **n_l** \\). 
The memory complexity in this case is \\( O( K **n_l** ) \\) where K is a constant, usually set to 256. 

**Performer**: uses random kernels to approximate the softmax in MSA. 

How to compare? It depends a lot on the trade-offs. More aggressive spatial resolution makes accuracy worst, but performance is much better (or memory cost manageable). 

Why is longformer better? 
Conv-like sparsity gives better inductive bias for ViTs. Or, the Longformer keeps keys and values at high resolution. 