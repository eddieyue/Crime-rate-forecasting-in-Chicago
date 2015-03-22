Crime Data
==========

I use the Crime data from Data Access Layer(DAL) https://github.com/cioc/DAL, which is a library that makes it easy to use the datasets. 

For this project, I work with the Chicago Crime dataset. The area of Chicago is partitioned into N = 2,985 square regions, with centers in the form of key-value pairs of latitude and longitude. And I will build up models and forecast for ten different crime types at Chicago:

ASSAULT, BATTERY,BURGLARY, CRIMINAL DAMAGE, DECEPTIVE PRACTICE,
MOTOR VEHICLE THEFT, NARCOTICS, OTHER OFFENSE, ROBBERY, THEFT 

The following bit of simple code to show how to extract and display them.

```python
from DAL import create
#create a handle to the crime dataset 
crime=create("crime")
#creates the Crime DAL.
crime.get_crime_list()->dict(key:int,value:string)
#gets the list of crime types.
crime.get_crime_counts()->dict(key:(int,int),value:[int])
#gets the number of crimes in each region. The first tuple value is the region and the second tuple value is the crime type.
crime.get_region_list()->dict(key:int,value:(float,float))
#gets the list of regions.
crime.iter()-> iterable(tuple(when:datetime.datetime,lat:float,lon:float,type:
str)
#iterates over all crimes in the dataset.
```

Kernel selection
================

I implement kernel smoothing to estimate a Poisson rate function parameter in next week. To apply kernel smiithing, I experiment different tuning parameters in Gaussian, Epanechinikov and Boxcar kernel. Then I select those produce the highest log-likelihood on held-out data.

Prediction of next week crime rates
===================================

For each of type of crime, I save my predicted rate for next week in a file, named as [crime-type].txt at all the regions in Chicago.