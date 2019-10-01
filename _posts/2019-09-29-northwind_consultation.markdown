---
layout: post
title:      "Northwind Consultation"
date:       2019-09-29 21:29:43 -0400
permalink:  northwind_consultation
---

As part of a project to review skills/understanding of exploratory data analysis (EDA), hypothesis testing, and communication with shareholders, I have been tasked with examining the Northwind Traders company and develop insights to help address growth issues.
Northwind Traders is an international importer/exporter of food products. Northwind has experienced a remarkable growth period during their most recent months. 
![](https://imgur.com/RlkG7Dh.png) <br />

This trend began in November of 2013 and continued until April of 2014. However, revenue has dropped considerably since then and I am tasked with examining the data they have provided to generate incites and recommendations to rectify this trend. 
## EDA
To get a better idea of deeper understanding of this trend, I have calculated the average daily revenue intake for Northwind and visualized it below:<br />
![](https://imgur.com/Bvem3aH.png)<br />
In recent months revenue day to day has not fluctuated greatly despite the considerable increase in revenue during that time. This suggests that the customer base has expanded, leading to the increased revenue as opposed to higher quantities of product in each order driving the increase. 
Plotting of each table within the database did not glean many useful insights as much of the data is categorical. Variables that were continuous were not normally distributed. As a result, non-parametric testing methods must be used to test our hypotheses.
## Hypothesis Testing
### Monte Carlos Simulations
Since our data is not normal, parametric hypothesis tests cannot be utilized for accurate examinations. An excellent alternative for statistical testing is the Monte Carlos simulation(MSC) which will be used extensively during my work with the Northwind database. This methodology entails repeated sampling of a population to obtain numerical results. I generated a function to maximize efficiency:
```
def monte(list1, list2, label):
    x=10000
    diff_mu_list1_list2 = np.mean(list1) - np.mean(list2)
    all_data =  list1 + list2
    diff_mu_list1_list2
    df = pd.DataFrame({'all_data':all_data})
    sample_a = df.sample(replace = False, n = len(list1))
    sample_b = df.drop(sample_a.index, axis = 0)
    sample_mean_diff = sample_a['all_data'].mean() - sample_b['all_data'].mean()
    sample_mean_diff
    sample_diffs = []
    counter = 0
    for i in range(x):
        sample_a = df.sample(replace = False, n = len(list1))
        sample_b = df.drop(sample_a.index, axis = 0)
        sample_mean_diff = sample_a['all_data'].mean() - sample_b['all_data'].mean()
        sample_diffs.append(sample_mean_diff)
        if sample_mean_diff < diff_mu_list1_list2:
            counter += 1
    plt.hist(sample_diffs);
    plt.axvline(diff_mu_list1_list2, color = 'red');
    plt.title(f' {label}\n {x} samples - p value {counter/x}');
    plt.show()
    beta = 1 - (counter/x)
    print('Beta value:', beta)
```

### Does discount amount have a statistically significant effect on the quantity of a product in an order? If so, at what level(s) of discount? <br />
* one-tail test
* H0: Discount amount plays no role in product quantity in an order.
* H1: Discount amount significantly affects product quantity in an order. <br />
![](https://i.imgur.com/UijCoXU.png)<br />
H1 was supported. Discount level played a significant role in increased product quantity across orders. Additionally, this effect was significant across every level of discount. An interesting thing to note is that though 10% discounts significantly, affected product quantity, it was to a lesser extent than all other discount levels. Further investigation is needed to grasp why this is the case.
<br />Recommendations: <br />
•	Use discounts to manage inventory
•	Further examine the role of discount in product quantity in regard to food category. 
o	may explain why 10% discounts display less efficacy
## Are discounted cereal/grains ordered in higher quantities than other discounted items?<br />
* one-tail test
* H0 Cereal/grains are not ordered at higher rates than other discounted items.
* H1: Cereal/grains, category 5 products, are ordered in higher quantities than other is supported.
![](https://imgur.com/idSrgiS.png)<br />
H0 was supported.  Cereal/grain were ordered in lower quantities compared to other categories of discounted items. In fact, Cereal/grain, category 5, was the lowest performing category in this regard.
<br />Recommendations: <br />
•	discontinue this discount
•	focus on growing product range in other categories
## Do countries outside of the U.S, have higher freight costs? <br />
* one-tail test
* H0: Countries outside the U.S. do not experience higher freight costs.
* H1: Countries outside the U.S. experience higher freight costs. <br />
H0 was supported. Countries outside of the U.S. do not experience higher freight rates. On average, their freight rates are actually lower than those of the U.S. Northern Europe and Western Europe have means that are statistically the same as that of U.S.
<br />Recommendations: <br />
•	Consolidated shipping
•	Marketing campaigns
•	Collect more data Eastern Europe
o	Make region a priority for marketing and exploratory sales
## What some categories of food product have higher discontinuation rates? <br />
* one_tail test
* $H_{0}$ No food categories have higher quatities of discontinued items.
* $H_{1}$ Some food categories have hgiher quantities of discontinued items.* H1 Some food categories have higher quantities of discontinued items. <br />
H0 was supported. No category of product was discontinued at a rate higher than the average. As such, no recommendations need be made.

