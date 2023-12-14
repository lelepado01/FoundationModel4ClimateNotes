# General Circulation Models


## Introduction

General Circulation Models (GCMs) are a class of models which use a combination of numerical solvers and tuned representations for small scale processes. 

## Neural GCM

> [Paper](https://arxiv.org/abs/2311.07222) |
[Code]()

Neural GCM is a GCM which uses a neural network to represent the small scale processes. 
It is competitive with ML models on 10 days forecasts, and competitive with IFS on 15 days forecasts.

Uses a fully differentiable hybrid GCM of the atmosphere, with a model split into two main subcomponents: 
- A **Differentiable Dynamical Core** (DDC) which solves the equations of motion (dynamic equations); 
- A **Learned Physics module**, which learns to parametrize a set of physical processes (physics equations) with a neural network.

## End-to-end training of GCMs

Uses extended backpropagation between the DDC and the Learned Physics module.

Three loss functions: 
- MSE for accuracy:
    Takes into account the layer lead time over the forecast horizon.
    Double penalty problem: wrong features at long lead times are penalized more than wrong features at short lead times.
- Squared Loss: 
    Encourages spectrum to match the data. 
- MSE for bias: 
    Batch average mean amplitude of the bias.

Trained on three days rollout data. 
Remained stable for year-long simulations.

## Stochastic GCM

Introduces randomness to be able to produce ensambles of forecasts.

Loss is *CRPS* (Continuous Ranked Probability Score) = Mean absolute error + Variance in ensamble spread