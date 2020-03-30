---
layout: post
title:      "Mental Health and Insurance Coverage within the U.S."
date:       2020-03-12 04:16:22 -0400
permalink:  under_construction
---


Over the past few years, insurance coverage , access to care, and mental health have become increasingly hot topics of discussion throughout the United States. As these topics are more deeply explored going forward, it makes sense to explore links between the two so a more informed discussion can be had. The present analysis will explore recent mental health issues, insurance coverage, and a recent lack in coverage. These links will be explored with information collected by the CDC. Specifically, the datasets utilized come from Behavioral Risk Factor Surveillance System (BRFSS). The BRFSS is a survey of telephone interviews conducted by state health departments across the US that began in 1984. For our purposes, focus will be on the years 2009 to 2018.

## Gathering the Data
I won’t bore you with all the gory details of acquiring the data. That could be its own blog. Long story short, a combination of Socrata API, requests, BeautifulSoup, and ZipFile allowed me to scrape and open all files needed to complete the project. Each year’s responses were saved as its own file and subsequently concatenated into one dataframe. Additionally, a full chronology of questions was saved as a separate data frame used to target questions pertinent to the present project. After some intensive cleaning, the final BRFSS response data frame had 4.5 million data points. 

![](https://imgur.com/9f9CVmx.png) 

## Methodology 
### Examining Regional Trends via Folium
To examine trends within our data at the regional level, Folium was used to visualize them. Below is an example of one of those visualizations:
>pop_participation = population[['STATE', 'Participation']]
>
>pop_participation.columns = ['STATE', 'Participation']
>
>url = 'https://raw.githubusercontent.com/python-visualization/folium/master/examples/data'
>state_geo = f'{url}/us-states.json'
>
>m = folium.Map(location=[48, -102], zoom_start=3)
>
>folium.Choropleth(
>   geo_data=state_geo,
>    name='Server Participation',
>    data=pop_participation,
>    columns=['STATE', 'Participation'],
>    key_on='feature.properties.name',
>    fill_color='RdPu',
>    fill_opacity=0.7,
>    line_opacity=0.2,
>    legend_name= 'BRFSS Respondents (SUM)').add_to(m)
>
>display(m)


![](https://i.imgur.com/J1SH3OK.png)

### Linking Mental Health to Insurance 
Logistical regressions were used to examine recent mental, and to some extent, physical ailments, in relation to insurance. Before developing the regressions, multicollinearity was addressed of course via heat maps. Example below:

Are recent displays of mental illness correlated with insurance coverage?

*NOTE: Refusals to respond, 9, was omitted from the models to minimize noise while addressing multicollinearity. Example of final output below:

![](https://i.imgur.com/m5HoEZp.png)

![](https://i.imgur.com/42kBXzO.png)


### Predicting Insurance Coverage and Recent Lack of Coverage
A suite of classification models were run to determine which performed best. Subsequently, hyperparameter tuning was done to optimize the selected models. The classification models utilized in the present analysis are below in addition to an example a classification model with its various accuracies, classification report, and confusion matrices before and after parameter tuning:

![](https://i.imgur.com/lpp5yrC.png)

## Conclusions

### U.S. Trends
Respondents in the southeast region of the U.S. have a lower perceived general health relative to the rest of the country. Moreover, those in the southeast are more likely to have recent mental or physical issues that affect their quality of life and ability to make decisions. An interesting thing to note is participants in the west, i.e. CO, CA, despite having higher levels of self reported health, have higher than average recent mental or physical issues. 


### Recent Mental Health and Insurance
In regards to mental health and insurance coverage, some predictions can be made. Recent mental health issues can be used to predict insured status (insured vs uninsured). An interesting thing to note was that receiving mental health treatment did not correlate with insured status. Respondents are receiving treatment regardless of insured status. Additionally, recent mental health issues can predict a lack of coverage in the past 12 months. 

### Predicting Insurance Status or Lack of Insurance
When developing the final classification models, downsampling had to be employed due to the highly imbalanced class distributions. Though our regression findings were promising, they did not translate to quality predictive models as neither of the hypertuned models cleared a 50% validation accuracy. 

![](https://i.imgur.com/H3oojqd.png?2)

The low quality of data likely played a considerable role in the lack of predictive power the classifiers could muster.

## Recommendations
1. Transition the BRFSS to an online format. This will allow for easier data acquisition that requires less manpower. Additionally, when online people tend to answer more honestly to higher levels of perceived anonymity. This could help cut down on the number of participants that refused to answer questions about their health.
2. Explore the use of an incentive to foster increased participation and honesty.  Money can be a good motivator but in small amounts so as not to skew responses.
3. Subsequent analysis of perceived health and its relationship to recent physical and/or mental ailments in U.S. populations that tend to see themselves as healthier should be explored. 

Though this analysis won’t quiet the current debates about mental health and insurance but, it can provide useful insights for a more informed discourse

Cheers.

