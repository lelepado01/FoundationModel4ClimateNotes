# Linear Transformers

> [Paper](https://arxiv.org/abs/2006.04768) |
[Code](https://github.com/Kyan820815/Linformer) |
[Explained](https://www.youtube.com/watch?v=-_2AF9Lhweo&list=WL&index=20&t=144s&pp=gAQBiAQB)

## Introduction

How to rout information in a sequence of tokens? -> We use query + key matrices

- Query: what we are looking for (what info we want to extract)
- Key: what type of info the node contains (what info we have)

Inner product is used to rout (similarity between query and key). 
This is called *soft-routing* as it is a weighted average of all the keys (where inner product is larger).

Complexity is \\( O(n^2) \\), where n is the number of tokens (sequence length), embedding size is d. 

\\( Q \times K = n \times n \\) -> where multi-head attention doesn't help, but the n matrix could be simplified into n/heads matrix.

Ex. 4 heads -> 512 / 4 = 128

We can approximate Q into a low rank matrix, and complexity would be reduced to \\( O(n) \\). 

## Linear Transformer

\\( \text{Attention} = \text{softmax}(\frac{QK^T}{\sqrt{d_k}})V \\)

If the term inside the softmax is low rank, then we can reduce computation. 

Eigenvalues of Q and K can be used to determine if matrix needs to be high or low rank.
Results show that most of the times 128 is enough.

How to reduce dimensionality?
We can use a random projection P before the self-attention layer. 
    
\\( \text{Attention} = \text{softmax}(\frac{Q(EK)^T}{\sqrt{d_k}})FV \\)

So we introduce the E and F matrices (fixed, not learned). The term inside the softmax becomes nxk, while FV is kxn. 
The shapes so are correct for matmult. 

## Results

With large sequence lengths, the linear transformer keeps inference times **constant**, as it doesn't depend on the sequence length n but also on k.
Complexity is reduced from \\( O(n^2) \\) to \\( O(nk) \\).

How to choose k?

\\( k = \frac{5\log(n)}{c} \\)

So it depends on n still? Complexity is \\( O(n\log(n)) \\) now.

However we can make it linear:

\\( k = min { \theta(9d \log(d)), 5\theta(\log(n)) } \\)

In the first case it is linear in d, in the second case it is linear in n.
We can choose the minimum of the two. So it's enough to downproject the matrix to a dimension of about d. 