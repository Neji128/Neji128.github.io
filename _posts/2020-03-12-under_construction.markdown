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
>    legend_name= 'BRFSS Respondants (SUM)').add_to(m)
>
>display(m)


![](https://i.imgur.com/J1SH3OK.png)

### Linking Mental Health to Insurance 
Logistical regressions were used to examine recent mental, and to some extent, physical ailments, in relation to insurance. Before developing the regressions, multicollinearity was addressed of course via heat maps. Example below:

Are recent displays of mental illness correlated with insurance coverage?

*NOTE: Refusals to respond, 9, was omitted from the models to minimize noise while addressing multicollinearity. Example of final result below:

![](https://i.imgur.com/m5HoEZp.png)

> clf_HLTHPLN1= BRFSS[['MENTHLTH', 'POORHLTH', 'QLMENTL2', 'MISTMNT', 'ADDEPEV2', 'DECIDE', 'HLTHPLN1']]
> 
> X = hlth_pln[['MENTHLTH', 'POORHLTH', 'QLMENTL2', 'MISTMNT', 'ADDEPEV2', 'DECIDE']]
> y = hlth_pln['HLTHPLN1']
> 
> X_train, X_test, y_train, y_test = train_test_split(X, y, random_state=0)
> 
> X = sm.tools.add_constant(X)
> logit_model = sm.Logit(y, X)
> result = logit_model.fit()
> result.summary()

![](https://i.imgur.com/42kBXzO.png)
### Predicting Insurance Coverage and Recent Lack of Coverage





