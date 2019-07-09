---
layout: post
title:      "King County Exploratory Data Analysis"
date:       2019-07-09 19:49:32 +0000
permalink:  king_county_exploratory_data_analysis
---


With our first project almost on the books, I felt it appropriate to go over my exploratory data analysis (EDA) and how I wanted to convey my findings to a non-technical audiences. Exploratory data analysis is a method of identifying and visualizing the characteristics of data sets and/or statistical models. 

The data set we used for our first project was the King County Housing data set. The data set is comprised of approximately 21,500 rows of data across 21 variables. this data was collected from May 2014 to May 2015 with data exploring living spaces within King county spanning from singular homes to data about the surrounding areas up to the neighborhood level. 
#### Correlation Heat Maps
Correlation heat maps allow us to visualize the strength of correlations between to variables using a color scale akin to infrared heat sensors. Light pink denotes a positive correlation, black indicates no correlation, light blue indicates a negative correlation. 
```
sns.heatmap(kc.corr(), center = 0) 
```
![](https://i.imgur.com/LNuK8Of.png)

There appears to be a large amount of collinearity among variables within the data set.  To create a model that is readily able to predict price outcomes, we must remove a few of the offenders. As a result, sqft_living15, sqft_above, bathroons, and grade were removed from the data set to help clean things up. 
#### Do higher condition scores and having a waterfront view raise the price of a house?
Boxplots assist in visualizing centrality of a data set in relation to the median in addition to providing insight into outliers and their prevalence. Keeping this in mind, I figured this would be an excellent way to examine the relationship house condition and possession of a waterfront view have on price. 
```
plt.figure(figsize=(12,12))
sns.boxplot(Ckc['condition'], Ckc['price'], hue=Ckc['Waterfront'])

plt.title('Price vs Condition/Waterfront', fontsize=16)

plt.ylabel('price')
plt.xlabel('condition')
plt.show()
```
![](https://i.imgur.com/HveummQ.png)

Homes of conditions 3+ were more expensive than of condition 2 or lower irrespective of waterfront status. Though the difference between median home price for conditions 3+ homes without waterfront were not markedly different. However, the median prices do display noticeable differences when homes do have waterfront views. Interestingly enough, condition 3 and 5 houses had higher median values than homes of condition 4. Maybe this is a phenomenon that can be examined more closely given more time later?
Another noteworthy phenomenon is the increase prevalence of outliers for conditions 3+ within the no waterfront view group. This could be route examined in further data analysis as well. 
#### Q-Q plots 
A Q-Q plot is a scatterplot that plots quantiles from 2 different data sets to one another. Ideally, the data points should follow a straight line. The variance from a straight path inform us of the normality of a distribution. Regarding the King county data set, we are testing residuals between the model and a normal distribution. 
```
resid = model.resid
fig = sm.graphics.qqplot(resid, dist=stats.norm, line='45', fit=True)
fig.show()
```
![](https://i.imgur.com/qXXzhTG.png)

The model above displays a highly skewed plot. This indicates that the model is not normally distributed. More than likely due to the results of there being so many outliers throughout my analysis. Most likely due to the large volume of outliers and the large range of price. 
So…what does this mean for the reliability of the model? Well, the model does have predictive abilities but, only to an exteme.
#### Does having more floors make house more expensive?
Typically homes with more floors are more expensive due, to the increased square footage the homes tend to have in addition to the higher consumption of materials, labor, and land required to build them. I thought it would be interesting to examine this question through the lens of the King County data set due to the higher population, housing density, and lower availability of land to build bigger homes. 
```
plt.figure(figsize=(12,12))
sns.boxplot(Ckc['floors'], Ckc['price'])

plt.title('Housing Prices by Number of Floor')
plt.xlabel(('floors').title())
plt.ylabel(('price').title())
plt.show()
```
![](https://i.imgur.com/Oj1rBGB.png)

An increasing number of floors did increase the median price of a home but, only to an extent. After 2.5 floors, homes actually displayed a decreased median price. Additionally, the inter quartile ranges for floors 3+ are lowest in the data set. Another notable phenomenon is the larger range between quartiles 1 and 3 within houses with 2.5 floors relative to other floor count houses. 
#### Do the lots owned around a home guide house price upward?
A scatter plots provide info concerning correlations between 2 variables in addition to providing insight into data skew.
 ```
plt.figure(figsize=(8,6))
plt.scatter(y='price', x='sqft_lot15', data=Ckc, alpha=.5)

plt.title('Housing Prices by Sqft of Lots')
plt.xlabel(('sqft_lot15').title())
plt.ylabel(('price').title())
plt.show()
```
![](https://i.imgur.com/ahTUEAT.png)

Hmm…looks like we have a bit to wade through here. It appears that the square footage of neighboring lots do not have a remarkable correlation with price. In fact, the highest value homes are in areas were the space of neighboring lots is extremely low, if not 0. Consequently, we cannot say that the lot size of neighbors necessarily affects house price. 
#### Final Thoughts
Based on the EDA, it appears that condition, waterfront status, and number of floors (to an extent), have a greater impact on house price relative to square footage of neighboring lot space. 

Additional analysis could be done on the number of floors a house has and its relation to price to gather a better understanding of the data set and its implications for subsequent studies. With another round of data cleanup, a more clear relationship between price and sqft_lot15 may be discernable. 

