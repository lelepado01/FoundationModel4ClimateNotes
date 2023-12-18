
# Structured State Spaces

> [Paper](https://arxiv.org/abs/2111.00396) | [Code](https://github.com/state-spaces/s4)

## Introduction

Especially suitable for long and continuous time series (speech, EEG, ...). 

Use seq to seq map to map input to a latent space.

```
<B, L, D> --> <B, L, D>
```

Much more efficient than Transformers, both computationally and memory wise. 
Also better at modelling long term dependencies.

``` admonish note
    The new model proposed is essentially a new layer. 
```


## Model

These are **continuous time models** (CTMs), which also allow for irregular sampling. 

State Space Models (SSM) are parameterized by matrices A, B, C, D, and map an input signal \\( u(t) \\) to
output \\( y(t) \\)  through a latent state \\( x(t) \\). Recent theory on continuous-time memorization derives special A matrices that allow SSMs to capture LRDs mathematically and empirically. (Right) SSMs can be computed
either as a recurrence or convolution.

Drawbacks are that are inefficient and prone to vanishing gradients. 
S4 introduces a novel parameterization that efficiently swaps between these representations, allowing it to handle a wide range of tasks, be efficient at both training and inference, and excel at long sequences.

Combine strength of the former models into State space models (SSMs): 
- Seq to seq: discretization of continuous sequence
- RNN: hidden memory state
- CNN: efficient computation and parallelization ability

\\( u(t) \leftarrow y(y) \\)

where \\( u(t) \\) is the input and \\( y(t) \\) is the output. 

\\( x'(t) = Ax(t) + Bu(t) \\)
\\( y(t) = Cx(t) + Du(t) \\)

where \\( x(t) \\) is the hidden state space, \\( u(t) \\) is the input, \\( y(t) \\) is the output we are trying to predict, \\( A \\) is the most important matrix called state matrix. 
\\( x(t) \\) can be a continuous function or a discrete sequence obtained by sampling.

How do we initialize the state matrix so that it handles long term dependencies?

(these matrices are not learned)

The Hippo approach allows memorization of the input (input reconstruction), even after a long time. It works by encoding the data with Legendre polynomials, which are orthogonal and can be computed efficiently. 
It allows to fully describe the input sequence even after long sequences. 

The idea is to condition A with low rank correction (computable as Cauchy kernel). 
A can be computed with the Hippo method, continuous time memorization (set of useful matrices).

- To discretize: sample from the continuous function \\( x(t) \\) at discrete time points \\( t_i \\)
    Convert A to discrete time matrix \\( \hat{A} \\) using the formula: 
    \\( \hat{A} = (I - \frac{\delta}{2}A)^{-1} (I + \frac{\delta}{2}A) \\)

- To convolution: simply unroll the timesteps into a single dimension and apply a convolutional layer, this allows parallelization


```admonish important
   With discrete representation, the efficiency is on par with RNNs. This is the reason the frequency domain is used to apply convolutions, which allows for efficient parallelization.
```


## Results

A general purpose model, which can be applied to continuous, recurrent and convolutional tasks and spaces. 
It is also efficient, both in terms of memory and computation, and performs better than other models (even transformers) on long sequences.