# Hiera ViT

## Introduction

Hiera ViT is a hierarchical vision transformer that removes additional bulk operations deemed unnecessary. 
Several components can be removed without affecting performance. 
This leads to a more simple and accurate model, which is also faster. 

## Hiera

Uses strong pretext task (with Masked autoencoder) to teach spatial bias. Local attention is used inside the mask units.

The problem when using masked autoencoders is the fact that we hide coarser information and we proceed deeper in the network. To avoid this, sparse masking is used (deletes patches, not overrides them). This also keeps the difference between token (internal feature representation of the model) and masked units (fixed size across layers). 

``` admonish note
MAEs are used beacuse they are effective teachers for ViTs.
```

The baseline used is MViTv2, which learns a multiscale representation of the image over 4 stages. First it learns low level features (but high spatial resolution), then at each stage trades channel capacity for spatial resolution. 

Pooling attention is used mostly to reduce the dimensionality of the input (especially for K and V, while Q is pooled to transition between stages by reducin spatial resolution).

## Simplifications

#### Relative Positional Embedding
This module was added to each attention block to allow the model to learn relative positional information. This is not necessary when training with MAEs, and absolute positional embeddings can be used. 

#### Remove Convolutions
Convolutions add unnecessary overhead since they provide benefits only when dealing with images. These are replaced with maxpools, reducing the accuracy of the model by 1.0%, however, when removing also maxpools with stride==1, the accuracy is nearly the same as the original one, but 22% faster.

#### Remove Overlap
Maxpools with 3x3 kernel size cause an issue of dimensionality, which is normally fixed with "separate and pad" technique. By avoiding overlaps between maxpools, this stage is unnecessary as kernel size equals to stride. The accuracy stays the same, but the model is 20% faster.

#### Remove Attention Residual
Attention residual is used as it helps to learn the pooling attention. It is used between Q and the layer output. 

#### Mask Unit Attention
Mask unit attention is used to learn the spatial bias as well as for dimensionality reduction (removing it would slow down the model). 
Instead local attention is used within the unit masks, so that tokens are grouped already once they arrive at the attention block. We can then perform attention within these groups (units). 

## Results

The model is 100% faster than the baseline, while remaining at the same accuracy for images. 

For videos, the model is 150% faster, and accuracy is increased by 2.5%.