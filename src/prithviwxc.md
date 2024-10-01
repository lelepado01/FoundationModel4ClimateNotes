
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

Pretraining with 2 phases: 
- 1. 5% drop path rate, 50% masking operator probability, alternates global and local attention masking. Uses random forecast lead time (0, 6, 12, 24 hours). Train on 64 A100 GPUs, Batch size = 1, ~100000 gradient steps.
