# Performer

Estimates regular self attention with provable accuracy in linear space and time complexity. 
Uses Fast Attention Via Orthogonal Random Features (FAVOR+) to approximate the softmax attention mechanism. (Scalable kernel method)

Normally attention is calculated as follows:

\\( Attn(Q, K, V) = D^{-1}AV \\)

Where \\( A = exp(QK^T / \sqrt{d}) \\) and \\( D = diag(A1_L) \\) (1 is a vector of ones)

The Performer approximates the softmax attention mechanism by using orthogonal random features. The attention mechanism is approximated as follows:

\\( Attn(Q, K, V) = \hat{D}^{-1}\hat{A}V \\)

Where \\( \hat{A} = tril(A) \\) and \\( \hat{D} = diag(\hat{A}1_L) \\), and *tril()* returns the lower triangular part of the argument matrix including the diagonal. 

The attention matrix can be calculated in \\( O(Ld^2 log(d)) \\) where \\( L \\) is the sequence length and \\( d \\) is the hidden dimension. While normally the attention matrix is calculated in \\( O(Ld^2 log(L) ) \\) time.