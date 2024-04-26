# Algal Bloom Forecast 2024 Erdos Project 
Algae blooms are dangerous for the public health and have recently become more frequent events. A predictive and/or explanatory analysis will be helpful for addressing this public health issue. There is NOAA data on several states (Florida, Texas, etc.) which could be augmented with supplementary weather data (climate change data).

## Authors
- [Deniz Olgu Devecioglu](https://github.com/heineborell)
- [Peter Doze](https://github.com/pddoze)
- [Nathanial Lowry](https://github.com/nLowry292)

## Overview:
Harmful algal blooms (HABs) occur when algae grows out of control and produce harmful toxins. These toxins contaminate the water we drink, and the local ecosystems, and have become a recurrent problem due to climate change.
The project goals are:
- What ecological features predict HABs?
- Can we use the available data to predict future HABs, so that the public can prepare itself.

## Stakeholders:
NOAA, State Tourism Board, Fish and Wildlife Department, local fisheries, coastal denizens.
## KPI:
Predicting/Forecasting an algal bloom accurately, building a model on more reliable measurements, predicting the severity of the bloom (duration and magnitude), predicting severe algal bloom events.

## Dataset
- The data is collected by [NOAA](https://www.ncei.noaa.gov/archive/archive-management-system/OAS/bin/prd/jquery/accession/download/120767/) (version 7) with a date ranging from 1950’s to 2023.  
- The  dataset covers algae cellcount, water temperature, salinity values.
- Data processing:
  - There were considerable number of NaN values in the dataset so we first checked the frequency of their occurence. 
  - The time intervals were uneven so the data are grouped with monthly and quarterly averages. In some cases we shorten the time interval for the training of the model. 
  - In order to capture a better correlation we also introduced a label called 'spike' which is defined to be any measurement that exceeds the average cell count up to the date of collection. 
  - We decided to forecast the algal blooms with Florida, the main source of the data.

## Approach
As we aim to predict future HABs the methods we utilize methods from the time series toolbox. With the exception of Random Forest, all methods employed are univariate, meaning they do not incorporate features for prediction. Here, we outline a summary of our employed strategies:

- **Baseline Forecasting**: Predicts algal blooms based on simpler methods. We used three baseline models: Naive, Average, and Trend baseline.
- **Exponential Smoothing**: Uses rolling average of previous data points to predict future data points with exponentially decreasing weights on the past data points. It is good for data with a strong underlying trend or seasonality or lack thereof, but it is a univariate model.
- **ARIMA**: Another univariate model, it interprets the time series data as a combination of past values plus an error term (AR). It looks at the difference between data metrics, such as the mean, through the dataset (I), and it looks at the datasets moving average (MA).
- **Random Forest**: Uses multiple decision trees to come to a singular result, making it our multivariate model. It allows us to incorporate water temperature and salinity data into our forecast.


