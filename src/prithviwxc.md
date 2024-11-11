
# PrithViWxC (NASA FM)

2.3B Params, 160 variables from MERRA-2 (New ERA5)

Encoder-decoder architecture (MAE) ~50% masking operator probability

Tested on: 
- Autoregressive rollout forecasting
- Gravity waveflux parameterization: small scale perturbations generated around thunderstorms
- Extreme event estimation

Max-ViT + HieraViT approaches: 
- Axial Attention (with convolutional layers)
- Add convolutions at finetune to improve performance 
- Local + Global attention
Uses Flash Attention and FSDP

Validation with: 
- Zero shot reconstruction
- Hurricane tracking
- Downscaling

MERRA2 dataset: cubed sphere grid, uniform grid spacing for each lat/lon (it minimizes grid spacing irregularities). 

Climatology: instead of predicting delta from current time, we predict the delta from historical climate C_t. It is calculated from merra with 61 days of rolling average (it is computed across space and time). 

Sigma^2_c = Sigma^2_c (x_t - C_t)

Normalization is also applied (10^-4 < sigma < 10^4, and 10^-7 < sigma_c < 10^7)

### Scaling and training

Pretraining with 2 phases: 
- 1. 5% drop path rate, 50% masking operator probability, alternates global and local attention masking. Uses random forecast lead time (0, 6, 12, 24 hours). Train on 64 A100 GPUs, Batch size = 1, ~100000 gradient steps.
- 2. 4 autoregressive steps with 80GB A100 GPUs. Use bfloat16 precision to shrink activation buffer sizes (and encoder / decoder size) while i/o remains f32
- 3. 2 phases in pretraining with different masking ratios and params

### Validation

- Masked reconstruction from zero-shot images
- Hurricane forecasting and tracking

Downstream applications: 
- Downscaling for 2m precision + climatelearn benchmark
- Finetune for cordex downscaling
- Zero-shot masked reconstruction --> excels at short lead time prediction from minimal data.