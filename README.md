# Data Alignment based on temperature data
## Introduction
A group of environmental scientists had a dataset of timestamped ecology images from Alaska.  They needed the timestamp to be accurate to the hour to process the images.  However, do to a faulty real-time clock the timestamps were not accurate.
One of the metadata recorded was temperature data.  My idea was to see if it was possible to match the temperature data with historical weather data collected at a nearby weather station.

## Methodology
I collected historical data collected by a nearby NOAA weather station (https://gml.noaa.gov/aftp/data/meteorology/in-situ/README).  I then cleaned up the temperature data and resampled to hourly temperatures.  I then designed an algorithm to match the temperature data.
I normalized both datasets and set any missing datapoints to 0.  Then I cut the temperature data into slices 24 hours long and 'roll' the slice along the NOAA data.  At each hour I compute the root mean square (RMSE) between the two values.  The date window with the lowest RMSE is considered the new timestamp.

## Results
Visually, you can see the time lag between the temperature data and the NOAA data.  Once the times were adjusted, the overlap was almost one-to-one.  Using this method, I was able to correct data collected from 2016-2022.

![comparison of NOAA and camera temperature](https://github.com/dcruzer231/date_alignment_based_on_temperature_data/blob/main/images/NOAA_temperature_phenocam_temperature.png)
![data aligned](https://github.com/dcruzer231/date_alignment_based_on_temperature_data/blob/main/images/data_aligned.png)


![data normalized](https://github.com/dcruzer231/date_alignment_based_on_temperature_data/blob/main/images/Normalized_temp_seg.png)

