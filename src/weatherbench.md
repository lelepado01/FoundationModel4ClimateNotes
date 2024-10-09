# WeatherBench

> [Paper](https://arxiv.org/abs/2002.00469) | [Code](https://github.com/pangeo-data/WeatherBench)


New benchmark to evaluate data-driven weather forecasting models (deep learning).
The benchmark task is to predict pressure and temperature 3-5 days in advance.

The dataset used is ERA5 (40 years), regridded to lower resolution (bilinear interpolation) and usinfg 13 height levels: 
- 5.625 degrees (32x64 grid)
- 2.8125 degrees (64x128 grid)
- 1.40625 degrees (128x256 grid)

Evaluation is executed on 2017 and 2018. 

RMSE is used as the evaluation metric, also latitude-weighted RMSE.

Baselines: 
- Operational NWP models (ECMWF, IFS)
- Linear Regression
- Simple CNN

### Weather Challenges

- 3D atmosphere (CNNs might not work if used as channels)
- Limited train data (samples are correlated in time)
- Data is heavy to store in GPU memory

Extreme situations forecast: used as validation, to make sure the model is not just blurring (averaging) the predictions.

### Key Features of WeatherBench
- Scientific Impact: of computing these models
- Challenge for data science
- Clear metrics for the climate domain
- Quickstart for users
- Reproducibility + communication between researchers