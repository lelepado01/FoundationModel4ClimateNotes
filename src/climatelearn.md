# ClimateLearn

> [Paper](https://arxiv.org/abs/2307.01909) | [Code](https://github.com/aditya-grover/climate-learn)

## Summary

Aims at aiding climate forecasting, downscaling and projections. 

It is a pytorch integrated dataset, composed mainly of **CMIP6**, **ERA5** and **PRISM** data.

- Forecasting: close to medium range weather and climate prediction
- Downscaling: Due to large grid sizes, large cells are often used for reducing size of data. However, this leads to loss of information, and to a lower resolution predictions. Downscaling aims at correcting bias amd map results to higher resolution.

    \\( C \times W \times H \leftarrow C' \times W \times H \\)
    where \\( H < H' \\) and \\( W < W' \\)

- Projections: Obtaining long range predictions under different conditions (ex. greenhouse gasses emission or atmosphere composition). 

The library also includes several baselines, pipelines for end-to-end training and evaluation, and a set of metrics.