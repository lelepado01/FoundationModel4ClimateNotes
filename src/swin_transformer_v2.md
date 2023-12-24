# Swin Transformer V2

> [Paper](https://openaccess.thecvf.com/content/CVPR2022/html/Liu_Swin_Transformer_V2_Scaling_Up_Capacity_and_Resolution_CVPR_2022_paper.html) | [Code](https://github.com/ChristophReich1996/Swin-Transformer-V2)

## Introduction

Swin Transformer V2 is an improved version of the Swin Transformer, which is a hierarchical vision transformer. It is designed to scale up to higher capacity and resolution. 

Some problems with the original Swin Transformer are:
- tranining instability
- resolution gaps
- hunger for labeled data

## Architecture and solutions

For the previous problems, the following solutions are proposed:

#### Residual post norm method

The residual post norm method is used to stabilize training. 
It replaces the pre-norm residual connection used in Swin Transformer with a post-norm residual connection.

The output of the residual block is normalized before merging with the main branch (amplitude of the main branch does not accumulate in the residual branch). 
This means the activation amplitudes are much milder, which makes training more stable.

#### Cosine Attention

Scaled cosine attention is used instead of dot product attention. 

\\( Sim(q_i, k_j) = \frac{cos(q_i, k_j)}{\tau} + B_{ij} \\)

where \\( B_{ij} \\) is the relative position bias matrix between pixels i and j, while \\( \tau \\) is a learnable scaling factor.

#### Log-Spaced continuous bias term

The coordinates are log-spaced, which allows for better resolution of the attention map.

\\( \hat{\Delta x} = sign(x) log(1 + \Delta x) \\)

where \\( \hat{\Delta} x \\) is the new log spaced coordinate, and \\( \Delta x \\) is the original coordinate.

The bias term also uses log-spaced continuous relative positions, instead of the parametrized approach. 

#### Self-supervised pre-training (SimMM)

This method avoids the need for many labeled samples. 


## Scaling up model capacity

The Swin Transformer V2 is scaled up by increasing the number of layers and channels. 
There are two main issues with this approach:
- Instability when increasing the number of layers: activations at deeper layers increase drammatically, creating a problem of discrepancy between layers of the network; 
- Degrade of performance when transfering to different resolutions. 