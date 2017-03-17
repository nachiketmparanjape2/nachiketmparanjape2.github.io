---
layout: post
title: "Time-Series Analysis - Stock Data"
date: 2017-03-03
---


### Welcome to my Stock Market Analysis Project!
I completed this project as a walk-through project during one of my courses. As my interest grew, I made great additions in the code using python as well as Tableau. Here is a brief summary of what I have done.

# Here's what I've done so far -
Here is the an overview of the data in this

<div class="update_box">
<p>

<div class='tableauPlaceholder' id='viz1489740388934' style='position: relative'><noscript><a href='#'><img alt='The Startup Quadrant ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Ve&#47;VentureCapitalists-Start-upFundingAdvice&#47;TheStartupQuadrant&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='site_root' value='' /><param name='name' value='VentureCapitalists-Start-upFundingAdvice&#47;TheStartupQuadrant' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Ve&#47;VentureCapitalists-Start-upFundingAdvice&#47;TheStartupQuadrant&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /></object></div>                <script type='text/javascript'>                    var divElement = document.getElementById('viz1489740388934');                    var vizElement = divElement.getElementsByTagName('object')[0];                    vizElement.style.width='1004px';vizElement.style.height='869px';                    var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script>

</p>
</div>

## [Tableau Dashboard](https://public.tableau.com/views/Shares-DailyOverview/Dashboard1?:embed=y&:display_count=yes)

, and this [Jupyter Notebook](https://github.com/nachiketmparanjape/Real_Time_Stock_Market_Analysis/blob/master/Stock_Market_Analysis.ipynb) contains my data exploration, analysis and visualization work for the project.


A template for time series analysis on the shares' data on any company.

## Here is an example for Ford Motors

#### The data fetched is from yahoo for the last 15 years

### Close
Closing prices are stationary
![closing-prices](https://cloud.githubusercontent.com/assets/11637437/23563095/0ce97f66-fffa-11e6-868b-fc68e1576ec8.png)

### First Difference

We can consider analyzing a first difference of the series. value of (t-1) is subtracted from value of (t).

![first-difference](https://cloud.githubusercontent.com/assets/11637437/23563098/0ceb2afa-fffa-11e6-91a5-d123249fa989.png)

First difference is relatively stationary and mostly fluctuates around 0. But variance of this series can vary over time. We need to incorporate mechanism to accomodate for sensing smaller variances along with the larger ones. Hence, Log.

### Log

Log of closing price

![log-closing-price](https://cloud.githubusercontent.com/assets/11637437/23563096/0ceaa97c-fffa-11e6-8308-3b150fbbca98.png)

So that gives us the original closing price with a log transform applied to <b>"flatten"</b> the data from an exponential curve to a linear curve. One way to visually see the effect that the log transform had is to analyze the variance over time. We can use a rolling variance statistic and compare both the original series and the logged series.


### Variance - with and without Log
![variance](https://cloud.githubusercontent.com/assets/11637437/23563103/0cfdbe04-fffa-11e6-805a-73b3094498fa.png)

![variance-log](https://cloud.githubusercontent.com/assets/11637437/23563101/0cfbad44-fffa-11e6-844c-9440efeb7dee.png)

### Normal and Logged First Difference
![normal-first-difference](https://cloud.githubusercontent.com/assets/11637437/23563102/0cfc4cea-fffa-11e6-8ad5-2f8fce20d87e.png)

![log-first-difference](https://cloud.githubusercontent.com/assets/11637437/23563100/0cedca08-fffa-11e6-8ab4-48fc744043df.png)

### Create a few more lag variables

Now we create a few more lab variables with lag of 1, 2, 5 and 30 days

![correlation-between-log-variables](https://cloud.githubusercontent.com/assets/11637437/23563097/0ceae2a2-fffa-11e6-892a-814d8908251c.png)

#### No apparent Correlation. It means that today's index values does not tell much about at least a few days in the future.

### Lag relationships

There could be relation in the values we did not try. There is a function to test those relationships. Let's try those.

![lag-correlation](https://cloud.githubusercontent.com/assets/11637437/23563099/0cebfc8c-fffa-11e6-8faa-3dbd730a3004.png)

### Seasonal Decomposition
 
![seasonal-decomposition](https://cloud.githubusercontent.com/assets/11637437/23563104/0cff2280-fffa-11e6-9bcf-8b30f208e991.png)

### ARIMA analysis

Analyis for perfomed, but as expected, it yielded inaccurate predictions. (Predicting shared ain't that easy!)
