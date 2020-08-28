---
published: true
---
**Contents**
* TOC
{:toc}

## Introduction

The goal of this project is to better understand the various cities around the globe. Global cities dataset contains sixty-nine cities worldwide and thirty-two feature.
After playing around with the dataset, and critically thinking about the various features, the seven most compelling variables in this dataset seem to be the *country, the city population size, the gross domestic product, life expectancy, the unemployment rate, the city area, and the annual population growth.*
In certain situations, it can be useful to compare countries rather than just individual cities when working with data on a global scale. 
Furthermore, the city population size and area are essential because they give information on how large a city is, how much space there is, and how crowded it is. For example, if a particular city has a much higher population size than another, but the area is much smaller, it gives a good idea of how the city must be organized to support such numbers.
The life expectancy and infant mortality also both can say a lot about a city. For example, life expectancy can be loosely tied with quality of life. This is because a poor and unhealthy life will lead to a shorter life expectancy. Infant mortality will also say a lot on this subject. Furthermore, high infant mortality rates are often associated with poor and unhealthy regions. Even if a city has a high GDP, a low life expectancy and/or infant mortality rate can say a lot about how most of the population is living. 
The unemployment rate is also an excellent indicator to learn more about an area, much like life expectancy. Unemployment rates can say a lot about the quality of life in the city and how it may be for the people who live there. Finally, a city's gross domestic product is a commonly used indicator of how the city is doing economically. It can be used to measure a city's success in terms different from the quality of life.

## Basic Visualizations

The first step involves reading in the data, and bringing in the libraries which will be used as well.

```R
# Reading in global cities data
globalCitiesData <- read.csv("GlobalCitiesPBI.csv")

# Bringing in neccessary libraries
library(knitr)
library(ggplot2)
library(stringr)
library(DMwR)
library(plotly)
```
The visualizations below show multivariate plots of the global cities dataset.
Life expectancy versus GDP is shown using a scatterplot because both axes' data comes in a continuous form that is not connected by time. Furthermore, the values have been organized by color using the continent of origin of each city. This helps provide further context to the plot and elaborates on the the nature of the data and why some points may be higher or lower than others. It can also show potential connections of the relationship between life expectancy and GDP to their geographical region. Different locations have different socioeconomic factors, and these can help further explain the relationship between the two primary variables shown.

[plot-1.png]({{site.baseurl}}/_posts/plot-1.png)






{% raw %}
<iframe width="450" height="400" frameborder="0" scrolling="no" src="//plotly.com/~hananather/1.embed"></iframe>
{% endraw %}
