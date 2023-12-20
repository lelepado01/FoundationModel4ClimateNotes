# Liquid Structured State Space Models

> [Paper](https://arxiv.org/abs/2209.12951) | [Code](https://github.com/raminmh/liquid-s4) 

## Introduction

Linear state space models have been used succesfully to learn representation of sequential data. 

In this approach, the structured state space model (S4) is combined with LTC space model to include the input dependant state-transition module. 
The liquid kernel structure takes into account the similarity between samples in sequences at train and inference time. 

## Continuous-time state space model

\\( \hat{x}(t) = Ax(t) + Bu(t) \\)
\\( y(t) = Cx(t) + Du(t) \\)

where \\( u(t) \\) is a 1d input signal, \\( x(t) \\) is the hidden state vector, \\( y(t) \\) is the output vector, and A, B, C, D are the system parameters.

The previous model can then be discretized using the Euler method:

\\( x_k = \hat{A}x_{k-1} + \hat{B}u_{k} \\)
\\( y_k = Cx_k \\)

where \\( \Delta t \\) is the time step, and D is equal to zero. 

And convolution can be applied to speed up the computation:

\\( x_0 = \hat{B}u_0, x_1 = \hat{AB}u_0 + \hat{B}u_1 \\)
\\( y_0 = \hat{CB}u_0, y_1 = \hat{CAB}u_0 + \hat{CB}u_1 \\)

The equation can be formulated as a convolutional kernel, which can be solved with a Cauchy kernel computation pipeline. 

The liquid linearized version of LTC is: 

\\( \frac{dx(t)}{dt} = - [ A + B \dot f(x(t), u(t), t, \theta) ] \dot x(t) + (\dots)\\)

where the term within square brackets is the LTC kernel. 

## Structured state space model + LTC Integration

We can integrate the LTC kernel into the S4 model by using a coupled bi-linear taylor approximation of the former equations. 

\\( \hat{x}(t) =[ A + Bu(t)] x(t) + Bu(t) \\)
\\( y(t) = Cx(t) \\)

Then we can discretize the previous equations using the Euler method:

\\( x_k = \hat{A} + \hat{B}x_{k-1} + \hat{B}u_{k} \\)
\\( y_k = \hat{C}x_k \\)

where \\( \Delta t \\) is the time step, and D is equal to zero.

And convolution can be applied to speed up the computation:

(other formulas)

\\( Y = \hat{K}u + \hat{K}_{liquid} u_{correlations} \\)

How do we compute the liquid kernel efficiently?

HIPPO matrix + NPLR representation + trainable B_n and P_n vectors. 

NPLR = low rank factorization \\( \leftarrow \\) diagonal + low rank matrices
