# PrIU: A Provenance-Based Approach for Incrementally Updating Regression Models

> [Paper](https://arxiv.org/pdf/2002.11791v1.pdf) | No code

## Introduction

PrIU is a provenance-based approach for incrementally updating regression models.

**Incremental view update**: iterative process of obtaining the best model for a given dataset, by training over and over removing small subsets. 

This paper proposes an efficient provenance-based approach to incrementally update model parameters without sacrificing accuracy (speedup of the train process). 
Enables provenance tracking and separates the contribution of each sample from the contribution of the model parameters (we can delete the training sample's effect). 

This is a framework for provenance tracking and how this can be used for fast model updates. The paper also proposes algorithms for fast model updates when removing a small subset of the training data. 

It also enables work on explainability and interpretability of AI models when removing data. 

## Provenance-Based Incremental Update

How to handle provenance matrices? 
- annotate input data with a set of *provenance tokens*
- propagate tokens through a set of operators: 
    - **+** which indicates an alternative 
    - **.** which indicates a join
- the application of these operations create *provenance polynomials*

TODO: continue reading from here