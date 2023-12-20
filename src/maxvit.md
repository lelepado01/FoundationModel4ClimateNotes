# MaxViT

> [Paper](https://link.springer.com/chapter/10.1007/978-3-031-20053-3_27) | [Code](https://github.com/google-research/maxvit)

Makes use of a new scalable attention model (multi-axis attention). 
- **Blocked local attention**: attention is only computed within a block of tokens.
- **Dilated global attention**: attend to some tokens is a sparse way.

Allows for linera complexity interactions between local/global tokens. 

Normally attention requires quadratic complexity, but this is reduced to linear complexity. Attention is decomposed into local and global attention (by decomposing spatial axis).

Given:

\\( x \in R^{H \times W \times C} \\)

- Normal attention flattens the H and W dimensions into a single one. 
- Block attention separates the token space into \\( < \frac{H}{P} \times \frac{W}{P}, P \times P, C > \\) non overlapping windows, each of \\( P \times P \\) size.
- Grid attention subdivides the token space into \\( < G \times G, \frac{H}{G} \times \frac{W}{G}, C > \\), where each grid point is uniformly spread over the token space. 

Using both block and grid attention, we can compute attention in linear time and have interaction between local and global tokens. 
Normally block attention underperforms on large token spaces, as it is not able to capture long range dependencies.
