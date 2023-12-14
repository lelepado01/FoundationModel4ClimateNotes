# ACE: A fast, skillful learned global atmospheric model for climate prediction

> [Paper](https://www.climatechange.ai/papers/neurips2023/14) | [Code](https://github.com/ai2cm/ace)

ACE is a global atmospheric model that uses a neural network to learn the dynamics of the atmosphere. 

- 200M parameters auto-regressive model
- 100 km resolution global atmospheric model
- 6 hours temporal resolution, stable for 100 years

## Model

The architecture uses a **Spherical Fourier Neural Transformer** (SFNT) to learn the dynamics of the atmosphere. 
This model uses a spherical harmonic transform of the grid, which is more suitable for the spherical geometry of the Earth. This enables more efficient computation of convolutions on spherical space.

The dataset used is **FV3GFS**, which is a global atmospheric model with 100 km resolution used as the US weather model. 

As normalization of samples, residual scaling is used. Where predicting an output always equal to the input for each variable would mean that each variable contributes equally to the loss (indipendently of the scale of variables).