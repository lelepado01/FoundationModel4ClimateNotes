# FuXi

> [Paper](https://arxiv.org/abs/2306.12873) | [Code](https://github.com/tpys/FuXi)

FuXi is an auto-regressive model for weather forecasting. The model is
based on the U-transformer architecture, and is able to recurrently produce a prediction for the next
timestep, given the previous predictions. 

![FuXi](../imgs/fuxi1.png)

To generate a 15 days forecast, it is estimated it takes the
model around 60 iterations, with a lead time of 6 hours. The loss utilized is multi-step, meaning it
takes into account several timesteps at once, minimizing the error for each of them. This is in contrast
with the approach taken in this project, where the loss is computed for each timestep individually. The
U-transformer takes as input around 70 variables, for the current timestep, as well as the the preceding
frame. All the variables used for this model are however restricted to two dimensions, ignoring any
height layer. This architecture is a variation of the vanilla transformer model, and as opposed to the
latter, before passing the encoded information to the self attention blocks, it downscales partially the
input.