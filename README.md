Crime Data
==========

I use the Crime data from Data Access Layer(DAL) https://github.com/cioc/DAL, which is a library that makes it easy to use the datasets. 

For this project, I work with the Chicago Crime dataset. The area of Chicago is partitioned into N = 2,985 square regions, with centers in the form of key-value pairs of latitude and longitude. And I will build up models and forecast for ten different crime types at Chicago:

ASSAULT, BATTERY,BURGLARY, CRIMINAL DAMAGE, DECEPTIVE PRACTICE,
MOTOR VEHICLE THEFT, NARCOTICS, OTHER OFFENSE, ROBBERY, THEFT 

The following bit of simple code to show how to extract and display them.

```python
from DAL import create

# Create a handle to the crime dataset 
crime=create("crime")

# Gets the list of crime types.
crime.get_crime_list()

# Gets the dictionary of number of crimes in each region. The first tuple value in key is the region, the second tuple value in key is the crime type and the value is the number of crimes.
crime.get_crime_counts()

# Gets the dictionary of regions with it's latitude and longitude.
crime.get_region_list()

# Iterates over all crimes in the dataset with the data time , latitude, longitude and type of crimes.
crime.iter()
```

Kernel selection
================

I implement kernel smoothing to estimate a Poisson rate function parameter in next week. To apply kernel smiithing, I experiment different tuning parameters in Gaussian, Epanechinikov and Boxcar kernel. Then I select those produce the highest log-likelihood on held-out data.

Prediction of next week crime rates
===================================

For each of type of crime, I save my predicted rate for next week in a file, named as [crime-type].txt at all the regions in Chicago. With the predicted crimes rate in all regions and their geographical information, it is easy to generate heat maps by heatmap.py, https://github.com/jjguy/heatmap.

Please check the notebook here for detail:

http://nbviewer.ipython.org/github/eddieyue/Prediction-of-crimes--location-and-rate--at-Chicago/blob/master/Forecasting%20of%20Crimes%27%20location%20and%20rate%20at%20Chicago%20.ipynb