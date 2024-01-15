# FireCast

> [Paper](https://www.ijcai.org/Proceedings/2019/0636.pdf) | [Code](https://github.com/HarguntasBenipal/FIREcast)

## Summary

FireCast is a CNN-based model for fire behaviour prediction.

30x30 window around epicenter of fire is used as input.

Ground truth is daily fire data (GeoMAC fire database). Weather data is used as input and has hourly temporal resolution. Uses LandSAT8 for satellite visual imagery, this is a 30 meter resolution dataset and they use rgb and near infrared channels. 

Weather variables include ATM pressure, humidity, temperature, precipitation, wind speed and dew point from NOAA. These variables have 3 km resolution, so pixels are interpokated to 30 m resolution.

Digital elevation model is used to extract elevation, slope and aspect from USGS national map.

Also MODIS burned are product collection 6 could be important, is available at GWIS (global wildfire information system).