# Linear Transformers as FWP

> [Paper](http://proceedings.mlr.press/v139/schlag21a.html) | [Code](https://github.com/ischlag/fast-weight-transformers)

## Introduction

The concept of fast weight programmers (FWP) is introduced in [this paper](https://arxiv.org/abs/1610.06258).

The idea is to use a **slow network** to program by gradient descent the weights of a **fast network**. FWP learn to pmanipulate the content of a finite memory and dynamically interact with it. 

Linear transformers have constant memory size and time complexity linear which depends on the sequence length. The time complexity is reduced thanks to the linearization of the self-attention layer and softmax operation.

## Linear Transformers as FWP

In normal neural networks, the weights are fixed and the input is manipulated, while the activation is input dependant and can change at inference time. 
The idea of FWP is also have the weights variable and input dependent (synaptic modulation). 

- Context-dependent -> slow weights
- Context-independent -> fast weights

The process revolves around a slow network which is trained to program the weights of the fast network. This makes the fast weights dependent on 
the spatio-temporal context of the input stream.

Which instructions to use? Outer product: 

\\( a^{(i)}, b^{(i)} = W_ax^{(i)}, W_bx^{(i)} \\)
\\( W^{(i)} = \sigma (W^{(i-1) + a^{(i)} \xor b^{(i)}}) \\)
\\( y^{(i)} = W^{(i)} x^{(i)} \\)

The outer product is \\( \xor \\), \sigma is the activation function, W_a and W_b are the trainable slow weights, while W is the fast weight matrix.

## Linearizing self-attention

Instead of removing the softmax, prior works have introduced techniques for linearizing the softmax.
This improves the computational efficiency of the self-attention layer for long sequences. 

An important term is the softmax kernel \\( \kappa(k, q) = exp(k \dot q) \\), which in linear self-attention is approximated by another kernel \\( \kappa'(k, q) = \fi(k)^T \fi(q) \\).

Since the embedding space for keys is limited, there is only room for d orthogonal vectors. If the length of the sequence is larger than d, th model might be in a overcapacity regime. In this case the model should dynamically interact with the memory content and determine which association to remember and which one to forget. 
On the other hand, the standard transformer stores associations as immutable pairs, increasing its memory requirements.
