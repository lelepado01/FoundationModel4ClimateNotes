# FourcastNet

> [Paper](https://arxiv.org/abs/2202.11214) | [Code](https://github.com/NVlabs/FourCastNet)

FourcastNet is an architecture based on the *Adaptive Fourier Neural Operator*, which is a neural network model designed for high-resolution inputs, fused with a
vision transformer backbone. The Fourier Neural Operator is a neural network architecture that uses
a Fourier basis to represent the input data, allowing for the efficient computation of convolutions in
the Fourier domain. 

![FourcastNet](../imgs/fourcastnet1.png)

The use of this module allows to have a very small footprint in GPU memory,
which is crucial for the training of large models. For instance, the base model used is
around 10Gb in size, while analogue models with similar number of parameters have a size of around
eight times as large.