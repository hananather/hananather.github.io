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

```r
# Plotting GDP and life expectancy using ggplot2
ggplot(data = globalCitiesData, mapping = aes(x = GDP.Per.Capita..thousands....PPP.rates..per.resident., y =Life.Expectancy)) + geom_point(aes(colour = Continent)) + xlab("GDP per Capita in Thousands") + ylab("Life Expectancy")+ ggtitle("Life Expectancy versus GDP") + theme_bw()
```
![plot-1]({{site.baseurl}}/images/Global_Cities/plot-1.png)


The plot of life expectancy versus the unemployment rate is built in the same way as the one above, which uses GDP. A scatter plot is optimal to display the potential relationship. Since the points can take on any value in a certain range, visualizations of the categorical kinds such as bar plots would not convey the information in the same effective manner.
```r
# Plotting unemployment rate and life expectancy
ggplot(globalCitiesData, mapping = aes(x = Life.Expectancy)) + geom_point(aes(y=Unemployment.Rate,colour=Continent))+ xlab("Life Expectancy") + ylab("Unemployment Rate")+ ggtitle("Life Expectancy versus Unemployment Rate") + theme_bw()
```
![plot-1]({{site.baseurl}}/images/Global_Cities/plot-2.png)


When visualizing a categorical and a continuous variable, bar plots can reveal a lot of information. The below plot gives the city population sizes for all the cities and has ordered them from largest to smallest. Finally, the legend also displays the Continent of each city once again. This visualization allows one to see which regions have the most populous cities and the sizes of each city exactly. A scatter plot in this scenario would show very similar data, but would not as effectively communicate the size differences in population per city due to the fact that this would be showed simply with the height of the point rather than with the dimensions of a bar of data as shown below.
```r
# Plotting city population size and continent
ggplot(globalCitiesData, aes(x=reorder(Geography,-City.Population..millions.),y=City.Population..millions.)) + geom_bar(stat="identity", aes(fill=Continent),colour="black", width=0.9)+theme(axis.text.x  = element_text(size=6.9)) + xlab("City Population Size") + ylab("City Population Size")+ ggtitle("City Population Sizes in Each Country")+theme(axis.text.x = element_text(angle = 90, hjust = 1)) + theme_bw() # (Chang, 2009), (zero323, 2015)
```
![plot-1]({{site.baseurl}}/images/Global_Cities/plot-3.png)
This next plot shows the city areas and population sizes per continent. This information is useful to split up because different regions tend to have distinct architectures and styles of living and differing amounts of physical space to expand in. This means that splitting the data per continent can help show the information in a context where it is easier to compare each city to those in geographically similar situations.
```r
# Plotting city areas and city population sizes split by continent

ggplot(globalCitiesData, aes(x = City.Area..km2., y =City.Population..millions., group=Continent)) +

geom_point(aes(colour = Continent)) + xlab("City Area in Kilometers Squared") + ylab("City Population in Millions")+ ggtitle("City Areas versus City Population Sizes Accross Continents") + theme_bw()+facet_grid(~Continent)+theme(axis.text.x = element_text(angle = 90, hjust = 1)) # (Chang,2009)
```
![plot-1]({{site.baseurl}}/images/Global_Cities/plot-4.png)

## Interactive Visualizations


The following plot shows the air quality within a city versus the GDP per Capita per person. This data was displayed in the form of a bubble plot since each city has values for air quality and gdp which both can take on any variable rather than being of a categorical nature. Furthermore, the size of each point changes based on the size of the population in each city. This helps provide further information and context to each value. 
The data for air quality was transformed in order to clarify the message of the graph further. The air quality index works by listing air quality on a scale of 0 to 500, with 0 being good and 500 being hazardous (US EPA, 2017). The problem with this is that using these values, one who is not familiar with the air quality index could believe that an extremely polluted city like Dehli for example, has good air quality since it is listed as 200 rather than understanding that this value is a bad sign. Therefore, a new column sorting the air quality is created to reduce confusion.

The plot is interactable, hover over points for more information and double click on elements in the legend to isolate and examine them.
```r
# Plotting GDP and air quality with bubble size as city population and colour as continent
p <- plot_ly(globalCitiesData, x = ~GDP.Per.Capita..thousands....PPP.rates..per.resident., y = ~Air.Quality., type = 'scatter', mode = 'markers',
        hoverinfo = 'text',
        color = ~Continent,
        marker = list(size = ~City.Population..millions., sizeref = 0.6, showlegend=F),
        text = ~paste('</br> City: ', Geography,
                      '</br> Country: ', Country,
                      '</br> Average Life Expectancy in Years: ',  Life.Expectancy))%>%
        layout(title = "Air Quality versus GDP per Capita in Global Cities",
           xaxis = list(title = 'GDP per Capita'),
           yaxis = list(title = 'Air Quality Index')) %>%
      layout(yaxis = list(
      ticktext = list("Good", "Moderate", "Potentially Unhealthy", "Unhealthy", "Very Unhealthy"), 
      tickvals = list(50, 100, 150, 200, 300),
      tickmode = "array"))  # (Plotly, 2019)
p
```
{% raw %}
<iframe width="800" height="500" frameborder="0" scrolling="no" src="//plotly.com/~hananather/5.embed"></iframe>
{% endraw %}


{% raw %}
<iframe width="800" height="500" frameborder="0" scrolling="no" src="//plotly.com/~hananather/1.embed"></iframe>
{% endraw %}
