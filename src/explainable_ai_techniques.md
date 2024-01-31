# Explainable AI Techniques 

> [Paper](https://d1wqtxts1xzle7.cloudfront.net/85521370/2111.14260v1-libre.pdf?1651739864=&response-content-disposition=inline%3B+filename%3DA_Practical_Tutorial_on_Explainable_AI_T.pdf&Expires=1706624636&Signature=CYUBdmJUk3fIPmHfZQiD9XFodWZC7~y-bDRJiA8yJc45PCmJnbR1EMpHt54PQqE1G3d3R3yVeyxBIfzSTX7H0Rb-m9hSTaTfMOZFodTktKSQYo4fyiE3cbfixfv~2oGADQvPM96M2Jj2ouIj3Wb2gceuv6pzbTB7A1E2LWp4Jx3NaxyahUM4S46WdoSkqdwku7c4KjCmxy~sPhGWyH5eyXixlVCkflOwPSNJGrEbWcEyocb9RllJSW7cYWoDuyIUClrkuKX7ShOUUpecKcihjS9SYWiMEE79b9jUMhe-~S1Sm4Su5ZV7XkISNGR8HXpemALWIb7O6~1WRiY0ttYvfA__&Key-Pair-Id=APKAJLOHF5GGSLRBV4ZA)

## Introduction

EXplainable Artificial Intelligence (XAI) techniques can serve to verify and certify model outputs and enhance them with desirable notions such as trustworthiness, accountability, transparency and fairness.

## Explainable AI Techniques

 - [SHAP](https://github.com/shap/shap)
 - [DiCE](https://github.com/interpretml/DiCE)
 - [GradCAM](https://keras.io/examples/vision/grad_cam/)
 - [Transformer Interpret](https://github.com/cdpierse/transformers-interpret)
 - [LTN](https://github.com/logictensornetworks/logictensornetworks)
 - [TS4NLE](https://github.com/ivanDonadello/TemplateSystemForNaturalLanguageExplanations)
 - [LRP](https://github.com/kaifishr/PyTorchRelevancePropagation)

## Explanations

### SHAP

SHAP (SHapley Additive exPlanations) is a model agnostic approach which decomposes the output of a model among all its input features. It is based on Shapley values from game theory. 
It performs an additive feature attribution analysis: 

\\( g(x) = \omega_0 + \sum_i^M{\omega_i x_i} \\)

where \\( \omega_0 \\) is the expected value of the model output as baseline, \\( \omega_i \\) is the contribution of feature \\( i \\) and \\( x_i \\) is the value of feature \\( i \\). 

SHAP has two inner models for each feature i, then computes the difference between both models' outputs. The difference is the contribution of feature i. 
The model yields the estimated feature importance by perturbing the input features and observing the change in the output. 

This method can visualize how much each feature changes the output of the model. 

This method only focuses on a model's inner functioning, no alignment with human expert explanation and reasoning is made.

### DiCE

DiCE (Diverse Counterfactual Explanations) is a model agnostic approach which generates counterfactual explanations from a set of events, given a model and a query.

This becomes an optimization problem, where the objective function is the distance between the counterfactual and the original instance. 

The final distance is calculated as a function of: 
- Diversity: encoded as the determinant of the covariance matrix of the counterfactual explanations

\\( dpp\_diversity(K) = det(K) \\)

where: \\( k = \frac{1}{1+dist(C_i, C_j)} \\) and \\( C_i \text{and} C_j \\) are counterfactual explanations. 

- Proximity: encoded as negative distance betweeen CFs features and the original input. 

\\( P = - \frac{1}{k} \sum_i dist(C_i, x) \\)

The final set of k CFs for the sample x is obtained by solving the following optimization problem:

\\( C(x) = argmin \{ \sum_k yloss(f(C_i, x)) + \sum dist(C_i, x) - \sum_k dpp\_diversity(C_1, ..., C_k) \} \\)

This method works well even for non-tech audiences. But only works for differentiable models, as it uses gradient descent.

### GradCAM

GradCAM (Gradient-weighted Class Activation Mapping) is a model agnostic approach which generates a heatmap of the input image, highlighting the regions that are important for the model's prediction. 
Gradients from any target create a localized map, which highlights the important regions for the target. This translates to which part of the image contributes more to the model's prediction.

Class Discriminative Localized map: 

\\( \alpha_k^c = \frac{1}{Z} \sum_i \sum_j \frac{\Delta y^c}{\Delta A_{i, j}^k} \\)

where \\( \alpha_k^c \\) is the importance of feature map (neuron importance) \\( k \\) for class \\( c \\), \\( \Delta y^c \\) is the change in class score (gradient for class c) and \\( \Delta A_{i, j}^k \\) is the change in activation map \\( k \\) at location \\( (i, j) \\).

This method offers a visual explanation. Lacks high resolution heatmap. 

### Transformer Interpret

Transformer Interpret is a model agnostic approach which is created ad-hoc for transformers. It is based on the attention mechanism of transformers, using the integrated gradents to map the importance of each token to the model's output. 

- Sensitivity: if a modification of a feature leads to a change in the classification output, then attribution is different from 0. The feature played a role in the classification.
- Implementation invariance: attribution method should not depend on model parameters. 

Integrated gradients adds sensitivity to the gradient based method by having a baseline. This way the model knows how the change in input influences the classification. 

This method can be used to interpret positive and negative attributions in output. 

### LRP

LRP (Layer-wise Relevance Propagation) produces a heatmap for every input data sample, highlighting the regions that are important for the model's prediction.

This method is good for any type of data. 

### LTN

LTN (Logic Tensor Networks) is a model agnostic approach which is based on first order logic. It is a neural-symbolic approach, which combines neural networks and symbolic reasoning. 
It involves costraint-based learning with FOL. 

It guaranties eterative exploration by saving each model parametrization, just by querying the model for an output. 

It tries to synthetize the model's reasoning with FOL. For each step of the network, it approximates the output of the network with a FOL formula. 

### TS4NLE

TS4NLE (Template System for Natural Language Explanations) is a model agnostic approach which generates natural language explanations for a given model and input. 

It is a technique to convert the explanation of an XAI to a natural language explanation. Can also be tailored to a specific domain or audience type.