---
layout: post
title:      "Histograms: An Statistical Staple"
date:       2019-06-18 18:51:15 -0400
permalink:  histograms_an_statistical_staple
---


At this point in life, a majority of us have encountered a histogram. But, not everyone knows what information we can glean from them. Why do we even need histograms in the first place? What do histograms tell us?

> ![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQpQMf3v4xMuE7dzWnlsrJvMpdZ9JFizpzNzou9fYwoUro-rIC8) Photo from Imgur

Histograms are a visual representation of frequency distributions, focusing on continuous data. These visualizations are especially useful for larger data sets. The area of each bar informs us of the frequency of occurrences within a bin, the range of divisions within a range of data, within the histogram. Additionally, histograms can identify outliers within raw data as well.

Another important aspect of histograms that provide information is their shape. The shape of a histogram allows statisticians and data scientist to make inferences about the skewness of data. This is important to note, as skewed data can lead to a model that is lacking in predictive power if not properly addressed early in model generation. There are quite a few different kinds of skewness, I however, will only discuss the most basic below:

> ![](https://asq.org/-/media/Images/Learn-About-Quality/Histogram/dcat-histogram-normal.gif?la=enhttp://) 
> 
> This is an example of a normal distribution. Please note, the 'bell-curve' pattern. Data is symmetrical and evenly distributed between both the left and right tails, i.e. extreme ends of the histogram. (Photo on ASW Quality Resources)

> ![](https://asq.org/-/media/Images/Learn-About-Quality/Histogram/dcat-histogram-right.gif?la=enhttp://) 
> 
> This is an example of right-skewed distribution. Note the skew towards frequencies at the higher end of the histogram range.
>![](http://) **Please note that this skew can favor the left side of a histogram as well leading to a left-skewed distribution.** (Photo on ASW Quality Resources)

So...what are the weaknesses of histograms as a data visualization tool? Histograms are not as versatile as say, a bar graph in regard to the variable types it can be used to visualize. Histograms focus on continuous variables. Additionally, bins in a histogram do not explicitly display frequency based on bar height, but the area within the bar as a function of the relationship between the bin range and Y. This can lead to misinterpretation by untrained eyes.
Histograms are part of the opening phases of data analysis. If used properly, they can set you up to successfully create a working model. Be mindful of the basics and take it slow. 


