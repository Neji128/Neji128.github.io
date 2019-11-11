---
layout: post
title:      "Zillow SARIMA Forecasting"
date:       2019-11-08 13:18:40 -0500
permalink:  zillow_sarima_forecasting
---

## Module 4 Project
<p>To develop a deeper understanding of Time-Series and data forecasting, I have been tasked with processing data from Zillow to find the 5 zip codes with the highest potential ROI for property development. Additionally, strategies to leverage this newly acquired information were requested as well. <p/>
### The Data
<p> The Zillow data set utilized comes from Kaggle and is readily available to replicate my processes. The data set contains housing data collected monthly from 1996 all the way to 2017. Data is within included space the state level down to zip code level. <p/>
<p>To create a more accurate model, data from 2009 onward will be included. The Great Recession of 2008 had a profound effect on the housing market and would muddy the water too much to create a reliable and accurate predictive model. Excluding this data is the best option to control for the uncertainty the recession would bring into the model. Additionally, the model will work with data from the metro level downward to focus the model. For out purposes, we will be using the Fayetteville, AR metro for model development. <p/>
<p> Overall, the data was pretty clean and uniform. ~~Thank gawd~~ Only one row of data had missing values. These values were filled with averages taken from the Fayetteville metro at large. Data was also converted from wide format to long format using function focused on melting data frames. <br\>
```
def melt_data(df):
    melted = pd.melt(df, id_vars=['RegionName', 'City', 'State', 'Metro', 'CountyName'], var_name='time')
    melted['time'] = pd.to_datetime(melted['time'], infer_datetime_format=True)
    melted = melted.dropna(subset=['value'])
    return melted.groupby('time').aggregate({'value':'mean'})
``` <p/> 
<p>  Another phenomenon of note was the high prevalence of stationarity among zip codes within the Fayetteville metro. The stationarity will be addressed by the I in the SARIMA model we are developing so this isn’t a terribly big deal. Just something to note.<p/>
![](https://imgur.com/zKsXYvp.jpg)<br \>

#### The Fayetteville Metro
<p>  The Fayetteville metropolitan area is an up and coming area of the U.S. being amongst the top 5 ‘best’ cities to move to for 5 years straight. Despite a dip in prices after the Great Recession, average home prices have consistently increased year over year since. An ideal environment for developing new properties based on our model. <p/>
![](https://imgur.com/VPHsQ8S.jpg)<br \>
### SARIMA Model
<p> The model developed for this project included a combination of SARIMA modeling, dynamic forecasting, traditional forecasting, and ROI calculations to identify zip codes with the highest potential ROIs in addition to the amount of risk incurred from investing in each of these zip codes. The biggest selling point of this model is that it identifies optimal parameters for the subsequent modeling of data. The top 5 zip codes identified are listed below in addition to an example of model output: <p/>
![](https://imgur.com/FfEBMV8.jpg)<br \>
![](https://imgur.com/HXs9sMz.jpg)<br \>
![](https://imgur.com/BdzeQYU.jpg)<br \>
![](https://imgur.com/PMq2kkR.jpg)<br \>
![](https://imgur.com/6lIIqlQ.jpg)<br \> 
<p> The model does a good job of standardizing our data as well as removing stationarity. The forecasting piece does a great job of identifying risks incurred by investing in each zip code. The best zip code to invest in within this scenario is 72701. This zip code significantly outperformed metro averages and had tight confidence indicated little to no loses should an investment be made, making it a very safe and reliable source of ROI. <p/>
![](https://imgur.com/R3wfp84.jpg)<br \>
#### Things To Consider
* A high ROI should not be the only consideration with this model. Consider the confidence intervals of your forecast. Intervals that are very wide or include values below actual data could mean loses.

