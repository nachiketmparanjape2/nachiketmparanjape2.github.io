---
layout: post
title: "Predicting Customers' Response to a Marketing Campaign"
date: 2017-08-23
---


Note : This [repository](https://github.com/nachiketmparanjape/Bank_UCI) contains the code, the jupyter notebooks, the images and a report for this project.

### Jump to

[Introduction](#introduction)

[Data Exploration](#data-exploration)

[Features and Machine Learning](#prep-and-data-science)


# Introduction
We all are familiar with the concept of [Telemarketing](https://en.wikipedia.org/wiki/Telemarketing). While it is an effective marketing tool for certain use cases, it is probably the slowest and most expensive in terms of outreach, as it involves company employee(s) manually contacting prospective consumers.

Hence, whenever a marketing campaign chooses this method, it makes sense if we try to maximize positive outcome by predicting the prospective-consumer behaviour using available data. In this particular case, I use a [dataset](http://archive.ics.uci.edu/ml/datasets/Bank+Marketing) from UCI's rich machine learning repository to predict consumer behaviour for a telemarketing campaign carried out for a term deposit. The dataset is rich with variety of financial, socio-economic as well as consumer history data.

Along with the primary goal of binary classification, we explore secondary qualitative insights about specific sections of societies that might respond to a specific type of marketing technique or a specific product. Let's start!

The [dateset](http://archive.ics.uci.edu/ml/datasets/Bank+Marketing) 41,188 datapoints with 20 attributes and one output variable.

#exploration
# Data Exploration

Let's see at some of the visualization that can help us to get a qualitative idea about the data, especially the categorical variables that are relatively easy to comprehend.

## Categorical Variables

### 1. Age
Kernel Density Estimation Plot with the hue of output variable 'y'

[insert image here]

We can see that the response is better from the people who are young (below 29) and old (above 60)

### 2. Job
Here is a bar plot representing proportional success for every profession category

[insert image here]

Students are Retirees are amongst the people most likely to subscribe (25-30% subscribed), whereas it was half as successful for the professions that are greater in numbers such as Administrators, Blue-Collar and Technicians.

### 3. Marital Status
How does it translate into successful subscriptions?

[insert image here]

The probability of acceptance is (4%) more for single people. Which corroborates the hypothesis that more students are accepting the subscriptions than the others.

### 4. Education
Proportion of people subscribed (left-y-axis) and Total number of people subscribed (right-y-axis) vs. Level of Education

[insert image here]

Here, 20% of illiterate population (total population is insignificantly small) seems to have subscribed. This can be a topic of study. If found substance, more illiterate people can be targeted to improve the overall response.

#### Hypothesis Test
Even though have very few illiterate people in our data (1014 datapoints or approximately 2.5% of the data), let's try testing our assumption using hypothesis testing.
**
1. Null Hypothesis - Probability of response is same for illiterate as well as other people
2. Alternate Hypothesis - Probability of response is more for illiterate people **

P-value for T-test turns out to be 7.25%. If we consider 5% as a threshold. So, unfortunately, we cannot rule out the null hypothesis.

### 5. Method of Contact

[insert image here]

Mean values for positive response are - 6% for telephone and 16% for cellular with relatively small std. Thus, we can assume an inclination towards cellular phone.

## Numerical Variables

** Correlation Heatmap **

[insert image here]

Following correlations seem strong -

* euribor3m - nr.employed - emp.var.rate
* previous - nr.employed
* cons.price.idx - nr.employed

Let's observe the correlations using lmplots from Seaborn library

[insert images here]

We can also see correlation between variables that seem visibly correlated in the heatmap by simply observing the corr dataframe

[insert image here]

# Prep and Data Science

As an initial step, I started with encoding categorical variables according to the type of category. The cateogorical variables that we have can further be divided subcategories as follows. The list contain description and the method of encoding -

** * Two Categories (default, housing, loan) **
Encoded by mapping 0 and 1 directly
** * Multiple Categories - no hierarchy (job, marital, contact, month, day_of_week, poutcome) **
Encoded by create a separate column for each category
** * Multiple Categories - hierarchy (education) **
Encoded by assigning levels in a single category (0,1,2,etc)

Then, all of these features along with numerical features were normalized between the range 0-1 to be used to train logistic regression, support vector machines as well as K-mean clustering. The data was used without normalization for decision tree based methods. Formula used for the purpose -

*z<sub>i</sub>=x<sub>i</sub>−min(x) / max(x)−min(x)*

Where,   *z<sub>i</sub>*- normalized value
         
         *x<sub>i</sub>* - value to be normalized
         
         *x* - array of numbers containing all the values of feature '*x*'







