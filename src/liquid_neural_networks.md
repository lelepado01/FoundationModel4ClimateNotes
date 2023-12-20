# Liquid Neural Networks

> [Paper](https://ojs.aaai.org/index.php/AAAI/article/view/16936) | [Code](https://github.com/mlech26l/ncps) |
[Explained](https://www.youtube.com/watch?v=IlliqYiRhMU&pp=ugMICgJpdBABGAHKBRVsaXF1aWQgbmV1cmFsIG5ldHdvcms%3D) 

## Introduction

In classical statistics there is an optimal amount of paramterers for a model, after which performance decreases. This problem is known as overparametrization and is also present in neural networks. The recent developments in transformers and vision transformers have shown that overparametrization can be beneficial for performance. 

Benefits include new emergent behaviours, more general learning and better generalization and robustness. This is at the cost of increased computational complexity and memory requirements, as well as lower accuracy on minority samples. 

Brain inspired, building blocks are neurons and equations from neuron to neuron. 

## Characteristics

Liquid neural networks stay adaptable even after training. 
Good for going out of distribution, so for real world applications (drone navigation, self driving cars).

Neural dynamics are continuous processes, so they can be described by differential equations.

``` admonish note
Synaptic release is more than just a scalar, and adds non-linearity to the system.
```

## Liquid State Machines

**Continuous time/depth neural networks** (CTRNNs) are a type of recurrent neural network (RNN) where the nodes (neurons) are described by differential equations.

\\( \frac{dx(t)}{dx} = f_{n,k,l}(x(t), I(t), \theta) \\)

Where f is the neural network, x is the state of the neuron, I is the input and \\(\theta\\) are the parameters of the network.

The state of the network is the state of all the neurons in the network.

There is no computation for each time step, the network is updated arbitrairly, unlike RNNs.

\\( \frac{dx(t)}{dx} = -\frac{x(t)}{\tau} + f_{n,k,l}(x(t), I(t), \theta) \\)

## Implementation

We need a numerical ODE solver, to resolve the differential equations.

The backward pass can either be done with the adjoint sensitivity method (loss + neural ODE solver + adjoint state) or with the backpropagation through time method (classic).
The latter method is considered better as it is not a black box. 

## Liquid Time-Constant Networks

**Leaky integrator neural model**

\\( \frac{dx(t)}{dt} = -\frac{x(t)}{\tau} + f_{n,k,l}(x(t), I(t), \theta) \\)

Uses conductance-based synapses, which are more biologically plausible than the classic synapses.

\\( S(t) = f_{n,k,l}(x(t), I(t), \theta)(A - x(t)) \\)

\\( \frac{dx(t)}{dt} = - [\frac{1}{\tau} + f_{n,k,l}(x(t), I(t), \theta)]x(t) + f_{n,k,l}(x(t), I(t), \theta)A \\)

The first term is time-dependent, while the second term the input representation at the current time step.

Activations are changed to differential equations, interactions are given by non-linearity (ex. neural nets). 

The network might associate the dynamics of the task with its own behaviour (ex. steering left/right implies camera movement).

The liquid time-constant (LTC) model is based on neurons in the form of differential equations interconnected via sigmoidal synapses.

Because LTCs are ordinary differential equations, their behavior can only be described over time. LTCs are universal approximators and implement causal dynamical models. However, the LTC model has one major disadvantage: to compute their output, we need a numerical differential equation-solver which seriously slows down their training and inference time. 

## Expressivity

Using the trajectory length method it is possible to measure the expressivity of a network.
The method consists in projecting the latent space of the network onto a lower dimensional space and measuring the length of the trajectory in the lower dimensional space (ex. 2D). 

These networks tend to have a higher expressivity than RNNs, but are bad with long term dependencies. 

Differential equations can form causal structures, which is good. 

Some limitations include: 
- the complexity of this network is tied to the ODE solver, which use fixed steps. Some solutions include Hypersolvers, closed form solutions and sparse flows.
- Vanishing gradients and exploding gradients are still a problem. A possible solution is to use a mixed memory wrapper.

## Neural Circuit Policies

**Neural Circuit Policies** are recurrent neural network models inspired by the nervous system of the nematode C. elegans. Compared to standard ML models, NCPs have

- Neurons that are modeled by an ordinary differential equation
- A sparse structured wiring
