# AICCA: AI-driven Cloud Classification Atlas

> [Paper](https://arxiv.org/abs/2209.15096v1) | [Code](https://github.com/RDCEP/cloud)

## Why?

Clouds are the cause of the most uncertainty in future climate projections. 

## Model + Dataset

It has been used a rotation invariant auto-encoder + hierarchical agglomerative clustering to capture the distinctions between cloud textures with just raw multi-spectral imagery. 

This was used to create a new cloud dataset (AICCA), consisting of AI generated clouds + labels for each cloud type sampled in 22 years of MODIS data. 
This is a NASA hosted aqua and terra satellite imagery dataset. 

## Training 

The first phase after obtaining the MODIS dataset is to train the RI autoencoder and then define cloud categories by clustering the compact latent representations produced by the trained autoencoder.
The latent space has to explicitly capture the variety of input textures among ocean clouds and also map to differences in physical properties. 

In addition, the use of a specific rotation-invariant loss function allows the model to lean in a way that is agnostic to orientation, for similar morphological clouds and thus places those similar clouds in the same cluster. 

## Assigning Clusters

Cloud clusters have to be:  
- **physically reasonable**
- capture information on **spatial distributions**
- **separable** and **rotationally invariant** 
- **stable** (produce similar or identical clusters when different subsets of the data are used)