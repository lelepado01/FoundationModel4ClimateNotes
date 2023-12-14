
# Structured State Spaces

> [Paper](https://arxiv.org/abs/2111.00396) | [Code](https://github.com/state-spaces/s4)

## Introduction

Especially suitable for long and continuous time series (speech, EEG, ...). 

Use seq to seq map to map input to a latent space.

```
<B, L, D> --> <B, L, D>
```

## Model

These are **continuous time models** (CTMs), which also allow for irregular sampling.

Drawbacks are that are inefficient and prone to vanishing gradients.

Combine strength of: 
- Seq to seq: discretization of continuous sequence
- RNN: hidden memory state
- CNN: efficient computation and parallelization ability

Combine strength of the former models into State space models (SSMs).

\\( u(t) \leftarrow y(y) \\)

where \\( u(t) \\) is the input and \\( y(t) \\) is the output.

\\( x'(t) = Ax(t) + Bu(t) \\)
\\( y(t) = Cx(t) + Du(t) \\)

where \\( x(t) \\) is the state, \\( u(t) \\) is the input, \\( y(t) \\) is the output, \\( A \\) is the most important matrix called state matrix. 

How do we initialize the state matrix so that it handles long term dependencies?

(these matrices are not learned)

The idea is to condition A with low rank correction (computable as Cauchy kernel). 
A can be computed with the Hippo method, continuous time memorization (set of useful matrices).

- To discretize: sample from the continuous function \\( x(t) \\) at discrete time points \\( t_i \\)
    Convert A to discrete time matrix \\( \hat{A} \\) using the formula: 
    \\( \hat{A} = (I - \frac{\delta}{2}A)^{-1} (I + \frac{\delta}{2}A) \\)

- To convolution: simply unroll the timesteps into a single dimension and apply a convolutional layer, this allows parallelization


## Results

A general purpose model, which can be applied to continuous, recurrent and convolutional tasks and spaces.