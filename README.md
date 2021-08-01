# Taxi Demand Forecasting
![image](https://user-images.githubusercontent.com/71088477/127751985-a80eafa7-ee49-4524-b169-def9c93875b5.png)

## Introduction
- The taxicabs of New York City are widely recognized icons of the city and come in two varieties: yellow and green. Taxis painted canary yellow (medallion taxis) are able to pick up passengers anywhere in the five boroughs. Those painted apple green (street hail livery vehicles, commonly known as “boro taxis”), which began to appear in August 2013, are allowed to pick up passengers in Upper Manhattan, the Bronx, Brooklyn, Queens (excluding LaGuardia Airport and John F. Kennedy International Airport), and Staten Island. Both types have the same fare structure. Taxicabs are operated by private companies and licensed by the New York City Taxi and Limousine Commission (TLC).

- Taxicab vehicles, each of which must have a medallion to operate, are driven an average of 180 miles per shift. As of March 14, 2014, there were 51,398 individuals licensed to drive medallion taxicabs. There were 13,605 taxicab medallion licenses in existence. By July 2015, that number had dropped slightly to 13,587 medallions, or 18 lower than the 2014 total. Taxi patronage has declined since 2011 due to competition from rideshare services.

## Business/Real World Problem
For a given location in New York City, our goal is to predict the number of pickups in that given location at particular time interval. Some location require more taxis at a particular time than other locations owing to the presence  of schools, hospitals, offices etc. The prediction result can be transferred to the taxi drivers via Smartphone app, and they can subsequently move to the locations where predicted pickups are high.


#### The end user for whom this case study is : Taxi driver

## Objectives:
- Our objective is to predict the number of pickups as accurately as possible for each region in a 10min interval. We will break up the whole New York City into regions, that we will discuss later in the blog. Now, the 10min interval is chosen because in NYC one can commute 1 mile in approximately 10 minutes given the traffic is normal at that particular time.

## Constraints:
- Latency: Given a location and current time of a taxi driver, as a taxi driver, he/she excepts to get the predicted pickups in his/her region and the adjoining regions in few seconds. Hence, there is a medium latency requirement.
- Interpretability: As long as taxi driver gets good prediction result, he/she is not be much interested in the interpretability of the result. He/she is not much interested in why he/she is getting this result. Hence, there is a no interpretability required.
- Relative Errors: Mean Absolute Percentage Error will be the relative error we will consider. Let say the predicted pickups for a particular location are 100, but actual pickups are 102, the percentage error will be 2% and Absolute error is 2. The taxi driver will be more interested in the percentage error than the absolute error. Let say in some region the predicted pickups are 250, and if taxi driver knows that the relative error is 10% then he/she will consider the predicted result to be in the range of 225 to 275, which is considerable.
- Our goal is to reduce the percentage error as low as possible.

## Data Information
To build this case study, we have some very interesting data from New York Taxi & Limousine Commission.These people regulate all the taxis in NYC and released the TLC TRIP RECORD DATA for yellow cab, green cab and FHV cab for public use.

### Information on taxis:
- Yellow Taxi: Yellow Medallion Taxicabs: These are the famous NYC yellow taxis that provide transportation exclusively through street-hails. The number of taxicabs is limited by a finite number of medallions issued by the TLC. You access this mode of transportation by standing in the street and hailing an available taxi with your hand. The pickups are not pre-arranged.
- For Hire Vehicles (FHVs): FHV transportation is accessed by a pre-arrangement with a dispatcher or limo company. These FHVs are not permitted to pick up passengers via street hails, as those rides are not considered pre-arranged.
- Green Taxi: Street Hail Livery (SHL): The SHL program will allow livery vehicle owners to license and outfit their vehicles with green borough taxi branding, meters, credit card machines, and ultimately the right to accept street hails in addition to pre-arranged rides.

## Libraries:
- dask: It is used to handle very large dataframes.
#### pip3 install dask
- folium: It is used to plot maps using latitude and longitude
#### i) pip3 install folium
#### ii) conda install -c conda-forge folium
- xgboost: It is used to make xgboost regression model.
#### i) pip3 install xgboost
#### ii) conda install -c conda-forge xgboost
- gpxpy: It is used while we calculate the straight line distance between two (latitude, longitude) pairs in miles.
#### pip install gpxpy

## Dask Library
Our data is very large in size. A single “csv” file is of more than 1GB in size, therefore loading all of the data at once using “Pandas” library will take up all of the RAM, and subsequently it will throw memory error. In order to overcome this problem, we are using dask library. Dask library is extremely useful library to use, particularly when we have data size larger than the RAM size. Dask does simple optimizations so that we can operate on data larger than the RAM size. Instead of loading all of the data at once in a RAM, dask load blocks of a file into RAM. It loads only those blocks of file that are required right now. As soon as the processing on the currently loaded block is done, it empties the RAM and load another block of file. This is how dask library is useful in working on data which are very large in size.

## Problem Formulation: Time Series Forecasting
### Given a region and a 10 min interval, we have to predict pickups.
- (a): How to break up the NYC into regions?
- (b): Every region of NYC has to be broken up into 10 min interval.

Now, every row pickup has longitude and latitude in it, and we will use this to define pickup regions.We already know, about the pickup at time ‘t’, we will predict the pickup at time ‘t+1’ in the same region. Hence, this problem can be thought of as a ‘Time Series Prediction’ problem. It is a special case of regression problems.

## Problem Formulation: Time Series Forecasting
### Given a region and a 10 min interval, we have to predict pickups.
- (a): How to break up the NYC into regions?
- (b): Every region of NYC has to be broken up into 10 min interval.

Now, every row pickup has longitude and latitude in it, and we will use this to define pickup regions.We already know, about the pickup at time ‘t’, we will predict the pickup at time ‘t+1’ in the same region. Hence, this problem can be thought of as a ‘Time Series Prediction’ problem. It is a special case of regression problems.

## Performance Metrics
1. Mean Absolute Percentage Error
2. Mean Squared Error

## Author
- Swetapadma Das
