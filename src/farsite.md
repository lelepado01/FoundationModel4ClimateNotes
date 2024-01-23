# FarSite

> [FarSite](https://data.fs.usda.gov/wwwbeta/sites/default/files/legacy_files/fire-management-today/059-2.pdf#page=13)

## Summary

Used for projecting the growth of natural fire. GIS data is used for landscape data. Weather + wind + landscape information is used to model fire growth. 

Uses Huygen principle of wave propagation to expand fire fronts. It treats the fire as a wave, points on edge are sources for the next timestep. Requires information only for points on the edge of the fire. 

> IS THIS APPROACH VALIDATED?

Each point on the edge contains information about the fire time, direction, rate of spread and intensity.

Can be expanded to include additional models, such as BURNUP model for fuel consumption, which is used for modelling post-frontal fire behaviour. These are activities occurring after the passage of the fire front (lack of data and analysis under this aspect). 

FarSite propagates the edge as an elliptical wavelet, where the wave shape is calculated as combination (additive) of wind speed and slope. 

Fire growth is the aggregate movement of all vertices along the fire edge during a timestep.