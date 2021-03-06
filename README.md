Crime Prediction
================

I use the Crime data from Data Access Layer(DAL) https://github.com/cioc/DAL, which is a library that makes it easy to use the datasets. 

For this project, I work with the Chicago Crime dataset. The area of Chicago is partitioned into N = 2,985 square regions, with centers in the form of key-value pairs of latitude and longitude. And I build up models and forecast for the following ten different crime types:

assault, battery, burglary, crimial damage, deceptive practice, motor vehicle theft, narotics, other offense, robbery, theft 

The following bit of Python code shows how to extract and display them:

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

I implement kernel smoothing to estimate a Poisson rate function parameter. To apply kernel smoothing, I experiment with different tuning parameters in Gaussian, Epanechinikov and Boxcar kernel. Then I select those producing the highest log-likelihood on held-out data.

Prediction of crime rates one week in advance
=============================================

For each of type of crime, I save my predicted rate for the following week in a file, named as [crime-type].txt. With the predicted crimes rate in all regions and their geographical information, I could have generated heatmaps by heatmap.py, https://github.com/jjguy/heatmap. However, due to the premission to access the data for now, the heatmaps are missing. I will fix it as soon as I get the permission to access the data.

Please check the notebook here for detail:

http://nbviewer.ipython.org/github/eddieyue/Crime-rate-forecasting-in-Chicago/blob/master/Forecasting%20of%20Crimes%27%20location%20and%20rate%20in%20Chicago%20.ipynb