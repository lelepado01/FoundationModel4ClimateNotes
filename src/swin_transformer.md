# Swin Transformer

> [Paper](https://openaccess.thecvf.com/content/ICCV2021/html/Liu_Swin_Transformer_Hierarchical_Vision_Transformer_Using_Shifted_Windows_ICCV_2021_paper) | [Code](https://github.com/microsoft/Swin-Transformer) 

## Introduction

Hierarchical Vision Transformer, representation is computed with shifting window. Self attention is limited non overlapping local windows. Allows for cross-window attention. 

``` admonish note
Features linear computational complexity. 
```

## Architecture

Patch size is 4x4 and 3 rgb channels. Linear embedding is applied to the patch, and size is constant C. 
Swin attention is then applied and patch merging is done for 2x2 neighboring patches.
Token reduction by 4: 

\\( \frac{H}{4} \times \frac{W}{4} \rightarrow \frac{H}{8} \times \frac{W}{8} \\)

Output dimension is set to 2C.

## Swin Attention

The swin transformer block replaces standard self attention with a sliding window attention, linear MLP layerm and GeLU activation function. Before attention layer normalization is applied.

The swin self attention is computed within a local window of size \\( M \times M \\), which makes it more scalable then normal self attention. 

This approach lacks connection cross window, so cross window attention is introduced. This method uses shifted windows partitioning, which alternates between two partitioning configurations. 
- Partition 8x8 feature map into 2x2 windows;
- Shift next layer from the previous by displacing the window. 

#### How to compute attention efficiently?

Several windows in the same batch can be created with with cycling shifting process. 

#### Relative Bias Problem

Add bias matrix B before softmax computation.

\\( Attn(Q, K, V) = softmax(\frac{QK^T}{\sqrt{d_k}} + B) V \\)

where B is a learnable matrix of size \\( M^2 \times M^2 \\), and \\( M^2 \\) is the number of patches in a window. 
This matrix can also be optimized by approximation, making it smaller with smaller window size: 

\\( B \in R^{M^2 \times M^2} \rightarrow B ~ \hat{B} \in R^{(2M-1) \times (2M-1)} \\)

## Variations of Swin Transformer model

| Model | C | Layer sizes | Parameters | 
|-------|-----|------------|--|
| Swin-B | 96 | <2, 2, 6, 2> | 29M |
| Swin-T | 96 | <2, 2, 18, 2> | 50M |
| Swin-S | 128 | <2, 2, 18, 2> | 88M |
| Swin-L | 192 | <2, 2, 18, 2> | 88M | 