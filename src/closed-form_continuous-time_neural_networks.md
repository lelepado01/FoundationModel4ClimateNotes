# Closed-form continuous-time neural networks

> [Paper](https://www.nature.com/articles/s42256-022-00556-7) | [Code](https://github.com/raminmh/CfC)

## Introduction

Closed-form continuous-time (CfC) models resolve the bottleneck of liquid networks (requiring a differential equation solver, which lengthens the inference and training time) by approximating the closed-form solution of the differential equation.

## Approximating Differential Equations

We need to derive an approximate closed-form solution for LTC networks. 

\\( x(t) = B \dot e−[wτ + f(x,I;θ)]t \dot f(−x, −I; θ) + A \\)

The exponential term in the equation drives the system’s first part (exponentially fast) to 0 and the entire hidden state to A. This issue becomes more apparent when there are recurrent connections and causes vanishing gradient factors when trained by gradient descent. 

To reduce this effect, we replace the exponential decay term with a reversed sigmoidal nonlinearity. 

The bias parameter B is decided to be part of the trainable parameters of the neural network and choose to use a new network instance instead of f (Bias).

We also replace A with another neural network instance, h(. ) to enhance the flexibility of the model. 

Instead of learning all three neural network instances f, g and h separately, we have them share the first few layers in the form of a backbone that branches out into these three functions. As a result, the backbone allows our model to learn shared representations. 

The time complexity of the algorithm is equivalent to that of *discretized recurrent networks*, being at least one order of magnitude faster than *ODE-based networks*.

## Problems

CfCs might express vanishing gradient problems. To avoid this, for tasks that require long-term dependences, it is better to use them together with mixed memory networks. 

Inferring causality from ODE-based networks might be more straightforward than a closed-form solution. 