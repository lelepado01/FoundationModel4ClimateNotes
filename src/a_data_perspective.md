# A Data-Oriented Perspective

## These are Data-Driven approaches

Here are the major climate-centered datasets used in the field:

| Dataset         | Size     | Where? |
|--------------|-----------|------------|
| MACCA | 60 TB | Nasa |
| CMIP6 | 25 TB |      |
| Earth System Configuration Grid | 25 TB | ORNL |
| ERA5 | 1.5 PB | ECMWF |
| ARM | 50 TB | ORNL |

Information as value chain: how information is created, stored, and used in a particular context.
 - How can we do this?
 - How are agencies taken from agencies and used in the field?
 - Is data free of errors?
 - Without any bias?
 - Is the data reliable?

# Model Summary

Here are some of the state-of-the-art models in the field and their performance:

| Model | Precision | Forecast time |
|--------------|-----------|------------|
| PanguWeather | < 50 m | 7 days |
| GraphWeather | < 50 m | 7 days |
| GraphCast | < 60 m | 8 days |
| ClimaX | < 100 m | 7 days |

Other approaches: 
 - Swin-SpatioTemporal Transformer: currently evaluated for NASA project 
    Higher complexity, better for small scale
 - Spherical Fourier Neural Transformer: to avoid noise and blurring problem
    Due to spherical projection of grid, problem is accentuated at the poles. 
    This model is able to avoid this problem, using this operator for sphere geometry.
 - GraphCast is better at small resolution and at different scales. 
    Also better at compressing information.
 - IFS uses global 9 km resolution data. On long term forecasts, it is better than ML models.
    However with higher resolution data (25km data), ML models are better.
 - Ensamble Forecasts: run several simulation from same initial conditions, and average the results.
    This is a common technique in NWP. Same approach can be used for ML models.
