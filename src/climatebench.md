# ClimateBench

> [Paper](https://agupubs.onlinelibrary.wiley.com/doi/full/10.1029/2021MS002954) | [Code]()

## Summary

The aim is to simulate shared socio-economic pathways. 

It is a benchmarking framework from **CMIP**, **AerChemMIP**, **ScenarioMIP**, and **Detection-AttributionMIP**.
It also contains several ML models and full complexity Earth System Models (ESMs).

Mostly used for long term projections.

Also includes *piControl* (pre-industrial control, 500 years of points) and *historical* (historical forcing) simulations, which can be used for contrastive learning to reduce the amount of samples required by ML models, as for projections not enough data is available for deep learning training.

A possible challenge is applying ML and statistical learning to high-dimensional data. To this end Linear Transformers could be used.