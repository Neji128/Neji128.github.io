---
layout: post
title:      "How Often Do You Eat Out? …Yes."
date:       2019-12-17 13:49:16 -0500
permalink:  cardiovascular_health
---

## Why logistic regressions are your friend in the face of vague data.
 
Ahh the doctor’s office, fluorescent lights and anxiety tinge the atmosphere from the waiting room to the sterile exam room. The medical information collected from patients verbally and physically inform physician diagnoses and subsequent treatment. This data is often a mix of objective and subjective data. Said data can be continuous or discrete depending on if measurements are taken, questions are asked, and the nature of said questions. This makes developing a model encompassing the data in its entirety tricky. An excellent example of said data can be found [here](https://www.kaggle.com/sulianova/cardiovascular-disease-dataset) will be used for the purposes of this blog. The GitHub repo for this project in its entirety can be found [here](https://github.com/Neji128/dsc-mod-5-project-online-ds-pt-051319). This is meant to be an overview of logistic regression and not an exhaustive dive. 

First things first, let's get a better look at our data. Per our output, there are numerous continuous and discrete variables that can be classified as objective data (measurements) or subjective data. Note the BMI feature was engineered during exploratory data analysis to help further data analysis. Additionally, age was converted to years for easier data consumption. 
 
```
population = pd.read_csv('cardio_train.csv', delimiter=';')
population.head()
population.set_index("id", inplace=True)
population.head()
```

 ![]( https://i.imgur.com/AXQGSsZ.png)

> NOTE: Though our dataset classifies cholesterol and glucose as examination features and they appear to be discreet, we have no idea where the cutoff’s or distributions are for ‘normal’, ‘above normal’, ‘well above normal’, as the cutoffs could be arbitrarily set for the purposes of data entry. As a result, we can’t conclude these are objective data despite numerical values being assigned.

What would happen if we run a linear regression on different data types? The first graph below illustrates the relationship between weight (continuous variable) and physical activity (categorical variable). The second graph illustrates the relationship between height (continuous variable) and weight (continuous variable). A linear regression in this scenario would be useless to glean any useful information unlike the second graph. No line drawn straight line drawn would display the relationship. This is where a logistic regression can move things into the right direction.

![](https://i.imgur.com/Hi00YD4.png)

Logistic regression, also known as a logit model, is a binomial regression model that allows us to create non-linear regression lines to get a more accurate understanding data interactions where both variables are note continuous in nature. A few key assumptions must be met.
### Logistic Regression Assumptions
1.	The target variable must be binary in nature i.e. 0s and 1s (In our case, yes or no)
2.	Observations must be independent of one another (Each of our patients is unique)
3.	Little but ideally no multicollinearity among independent variables 
For our purposes, the first 2 conditions are met. We can check for multicollinearity using a heatmap.

![]( https://i.imgur.com/m8RbbVH.png)

It looks like height, weight, and BMI are highly correlated. We will need to isolate BMI via a second logit model. Once our variables are isolated, we can produce said models. Both examples are included below:
#### CD model (BMI)
```
X = population.drop(['cardio', 'BMI'], axis =1) 
y = population['cardio']

X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=0)

X = sm.tools.add_constant(X)
logit_model = sm.Logit(y, X)
result = logit_model.fit()
result.summary()
```

![](https://i.imgur.com/z0o6rAa.png?1)

#### CD model (Height/Weight)

```
X = population.drop(['cardio', 'weight', 'height'], axis =1) 
y = population['cardio']

X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=0)

X = sm.tools.add_constant(X)
logit_model = sm.Logit(y, X)
result = logit_model.fit()
result.summary()
```

![](https://i.imgur.com/wc2HRWd.png?1)
 
Another great use for logistic regressions is examining interactions between variables as well. Interactions can be an important aspect of EDA; deeper insights can be developled for delivery target audience no matter their technical expertise. The example below illustrates this well: 

```
X = population[['cholesterol', 'active']]
#engineering interaction between cholesterol and pyhsical activity
X['cholesterol_active'] = X['cholesterol'] * X['active']
y = population['cardio']
 
X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=0)
 
X = sm.tools.add_constant(X)
logit_model = sm.Logit(y, X)
result = logit_model.fit()
result.summary()
```

![](https://i.imgur.com/xpSLu2w.png)

Hopefully, this loose guide was able to help you better understand the purpose of logistic regressions in the face of vague binary data. Don’t be afraid to provide any feedback or insights you may have. 






