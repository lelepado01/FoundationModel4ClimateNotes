# MetNet 3 

> [Paper](https://arxiv.org/abs/2003.12140) | [Code](https://github.com/lucidrains/metnet3-pytorch)

- Temporal resolution: 2 minutes
- Spatial resolution: 1 km

The network is a U-Net in conjunction with a MaxVit architecture

- **Topographical embedding**: automatically embeds time-indipendent variables (4km tokens) for 20 parameters
- **U-Net**: based on a fully convolutional neural network whose architecture was modified and extended to work with fewer training images and to yield more precise segmentation
- **MaxVit**: hybrid (CNN + ViT) image classification models.

Uses parameter oriented training for lead time (0 - 24 hours). 
Masks out with 25% probability a block of data. 
