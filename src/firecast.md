# FireCast

> [Paper](https://www.ijcai.org/Proceedings/2019/0636.pdf) | [Code](https://github.com/HarguntasBenipal/FIREcast)

## Summary

FireCast is a CNN-based model for fire behaviour prediction. Combines GIS satellite imagery and weather data with AI to predict fire behaviour. Location characteristics are extracted from Landsat8 images + elevation data (DEM). Weather data is extracted from NOAA (wind + temp + humidity).

The model is a CNN trained to predict the next 24 hour's fire perimeter. 
Each window is composed of 30x30 pixels around epicenter of fire and is used as input.
GT is from GeoMAC fire database. Landsat8 is used for satellite visual imagery and downloaded from GloVis (uses rbp and near-infrared). DEM is from USGS national map. Weather data is from NOAA.

Ground truth is daily fire data (GeoMAC fire database). Weather data is used as input and has hourly temporal resolution. Uses LandSAT8 for satellite visual imagery, this is a 30 meter resolution dataset and they use rgb and near infrared channels. 

Weather variables include ATM pressure, humidity, temperature, precipitation, wind speed and dew point from NOAA. These variables have 3 km resolution, so pixels are interpokated to 30 m resolution.

Digital elevation model is used to extract elevation, slope and aspect from USGS national map.