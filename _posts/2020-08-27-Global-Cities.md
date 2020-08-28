---
published: true
---
* TOC
{:toc}


## Introduction

The global cities dataset lists cities accross the world and gives different types of information about them. This information includes things like continent, city population size, life expectancy, etc... Of this information, the seven most important variables in this dataset are the country, the city population size, the gross domestic product, life expectancy, the unemployment rate, the city area, and the annual population growth. 
  The country of the city is the most important geographic indicator for this data because when comparing data on a global scale, it is much more useful to compare at a higher level than individual city. Furthermore, The city population size and area are both important because they give information on how large a city is, how much space there is, and therefore how crowded it is as well. For example, if a certain city has a much higher population size than another, but the area is much smaller, it gives a good idea as to how the city must be organized to support such numbers.
  The life expectancy and infant mortality also both can say a lot about a city. For example, life expectancy can be loosely tied with quality of life. This is because a poor and unhealthy life will lead to a shorter life expectancy. Therefore, this value is a good indicator of this characteristic in a city. Infant mortality will also say a lot on this subject. Furthermore, high infant mortality rates are often associated for poor and unhealthy regions. Even if a city has a high GDP, a low life expectancy and/or infant mortality rate can say a lot about how the majority of the population is living. 
  The unemployment rate is also a good indicator to learn more about an area, much like life expectancy, unemployment rates can say a lot about the quality of life in the city and how it may be for the people who actually live there. Finally, the gross domestic product of a city is a commonly used indicator for how the city is doing in economic terms. It can be used to measure the success of a city in terms different from the quality of life.

## Basic Visualizations

The first step involves reading in the data, and bringing in the libraries which will be used as well.
```
# Reading in global cities data
globalCitiesData <- read.csv("GlobalCitiesPBI.csv")

# Bringing in neccessary libraries
library(knitr)
library(ggplot2)
library(stringr)
library(DMwR)
library(plotly)
```




{% raw %}
<iframe width="900" height="800" frameborder="0" scrolling="no" src="//plotly.com/~hananather/1.embed"></iframe>
{% endraw %}

