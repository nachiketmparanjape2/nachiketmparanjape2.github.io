---
layout: post
title: "Predicting Customers' Response to a Marketing Campaign"
date: 2017-08-23
---


Note : This [repository](https://github.com/nachiketmparanjape/Bank_UCI) contains the code and the jupyter notebooks. This is the [report](https://docs.google.com/document/d/1xeAxD7FS3owV1hpMB-60B5gfO7iFvREwQ2YPB1Qp_co/edit?usp=sharing).

### Jump to [Data Exploration](#data-exploration) or [Features and Prediction](#features-and-prediction)

# Introduction
We all are familiar with the concept of [Telemarketing](https://en.wikipedia.org/wiki/Telemarketing). While it is an effective marketing tool for certain use cases, it is probably the slowest and most expensive in terms of outreach, as it involves company employee(s) manually contacting prospective consumers.

Hence, whenever a marketing campaign chooses this method, it makes sense if we try to maximize positive outcome by predicting the prospective-consumer behaviour using available data. In this particular case, I use a [dataset](http://archive.ics.uci.edu/ml/datasets/Bank+Marketing) from UCI's rich machine learning repository to predict consumer behaviour for a telemarketing campaign carried out for a term deposit. The dataset is rich with variety of financial, socio-economic as well as consumer history data.

Along with the primary goal of binary classification, we explore secondary qualitative insights about specific sections of societies that might respond to a specific type of marketing technique or a specific product. Let's start!

The [dateset](http://archive.ics.uci.edu/ml/datasets/Bank+Marketing) 41,188 datapoints with 20 attributes and one output variable.

# Data Exploration

Let's see at some of the visualization that can help us to get a qualitative idea about the data, especially the categorical variables that are relatively easy to comprehend.

## Categorical Variables

### 1. Age
Kernel Density Estimation Plot with the hue of output variable 'y'


![age-kde-plot](https://user-images.githubusercontent.com/11637437/29989346-372e8084-8f27-11e7-8d06-18942a7ea83e.png)

We can see that the response is better from the people who are young (below 29) and old (above 60)

### 2. Job
Here is a bar plot representing proportional success for every profession category

![job-bar-plot](https://user-images.githubusercontent.com/11637437/29989355-47633008-8f27-11e7-92a9-72bec9c3e513.png)

Students are Retirees are amongst the people most likely to subscribe (25-30% subscribed), whereas it was half as successful for the professions that are greater in numbers such as Administrators, Blue-Collar and Technicians.

### 3. Marital Status
How does it translate into successful subscriptions?

![marital-status-plot](https://user-images.githubusercontent.com/11637437/29989360-50ec8f48-8f27-11e7-990f-95b770601430.png)

The probability of acceptance is (4%) more for single people. Which corroborates the hypothesis that more students are accepting the subscriptions than the others.

### 4. Education
Proportion of people subscribed (left-y-axis) and Total number of people subscribed (right-y-axis) vs. Level of Education

![education-plot](https://user-images.githubusercontent.com/11637437/29685189-8e484bd4-88c9-11e7-8f68-3efcec61914b.png)

Here, 20% of illiterate population (total population is insignificantly small) seems to have subscribed. This can be a topic of study. If found substance, more illiterate people can be targeted to improve the overall response.

#### Hypothesis Test
Even though have very few illiterate people in our data (1014 datapoints or approximately 2.5% of the data), let's try testing our assumption using hypothesis testing.

1. **Null Hypothesis - Probability of response is same for illiterate as well as other people**
2. **Alternate Hypothesis - Probability of response is more for illiterate people**

P-value for T-test turns out to be 7.25%. If we consider 5% as a threshold. So, unfortunately, we cannot rule out the null hypothesis.

### 5. Method of Contact

![method-of-contact-plot](https://user-images.githubusercontent.com/11637437/29989381-6894d7f4-8f27-11e7-9851-34d446e3e0f3.png)


Mean values for positive response are - 6% for telephone and 16% for cellular with relatively small std. Thus, we can assume an inclination towards cellular phone.

## Numerical Variables

** Correlation Heatmap **

![numerical-colormap](https://user-images.githubusercontent.com/11637437/29989377-6580e332-8f27-11e7-83bc-da5d26e0e26a.png)

Following correlations seem strong -

* euribor3m - nr.employed - emp.var.rate
* previous - nr.employed
* cons.price.idx - nr.employed

Let's observe the correlations using lmplots from Seaborn library

![scatter-4](https://user-images.githubusercontent.com/11637437/29685202-95191f2e-88c9-11e7-80f4-4e153513ab50.PNG)

We can also see correlation between variables that seem visibly correlated in the heatmap by simply observing the corr dataframe

![table](https://user-images.githubusercontent.com/11637437/29685203-96327fc2-88c9-11e7-9de9-42f3df408840.png)

# Features and Prediction

As an initial step, I started with encoding categorical variables according to the type of category. The cateogorical variables that we have can further be divided subcategories as follows. The list contain description and the method of encoding -

 * **Two Categories (default, housing, loan)**
 
Encoded by mapping 0 and 1 directly
* **Multiple Categories - no hierarchy (job, marital, contact, month, day_of_week, poutcome)**

Encoded by create a separate column for each category
* **Multiple Categories - hierarchy (education)**

Encoded by assigning levels in a single category (0,1,2,etc)

Then, all of these features along with numerical features were normalized between the range 0-1 to be used to train logistic regression, support vector machines as well as K-means clustering. The data was used without normalization for decision tree based methods. Formula used for the purpose -

<p align="center"><em> z<sub>i</sub>=x<sub>i</sub>−min(x) / max(x)−min(x) </em></p>

Where,  *z<sub>i</sub>*- normalized value;     *x<sub>i</sub>* - value to be normalized;     *x* - array of numbers containing all the values of feature '*x*'


I deleted the datapoints corresponding to 71 missing datapoints in "marital" as well as 330 datapoints in the "job" columns. For the rest of the missing data _(default : 8597, housing : 990, loan : 990, education : 1596)_, I used random forest to populate the missing space with predicted values.
      
------

After the data was cleaned and features were finalized, we employed logistic regression, support vector machines and a few varieties of ensemble methods using decision trees. As the decision trees with gradient boosting performed well, let's use that model from now on to assess performance.

When the model was tuned for overall accuracy score, an accuracy score of 90.05% was achieved. It is a very good result to start with. Also, when we dive in a little deeper and observe the recall scores within the positive and negative responses, here’s an example of the result for the model optimized for overall accuracy score -

![result_1](https://user-images.githubusercontent.com/11637437/29794671-d5d18c04-8bfd-11e7-962a-2e4ba7869180.PNG)

As we can see from the data, although the accuracy score is good, we see from the confusian matrix as well as recall score that 80% of the positives wrongly predicted as negatives. To put that in other words, we still have a large proportion of false negative and for our prediction model to be more useful we need to minimize that number, which implies maximizing recall while minimizing the possible increase in false positives. But, in our case, even if we end up increasing comparable numbers of false positives and true positives, it will still be more useful to us than the current model.

Hence, to improve recall I used a two step-approach -

### New Features

**1. I binned a few numerical features to convert them to categorical as follows -**
<ol>
<li> pdayscat - Converted pdays into a binary category
 <ol>
 <li> Customer was not contacted for previous campaign (pdays = 999) </li>
 <li> Customer was contacted for previous campaign (pdays != 999) </li>
 </ol>
</li>
      
<li> agecat - Converted age into 3 categories based on observation </li>
  <ol>
  <li>age <= 23</li>
  <li>23 < age < 62</li>
  <li>age >= 62</li>
  </ol>
</li>
 
<li> campcat - Converted Campaign (number of contacts performed during this campaign and for this client) into a binary category based on observation
  <ol>
  <li>campaign <= 12</li>
  <li>campaign > 12</li>
  </ol>
</li>
</ol>

**2. Clustering for Feature Extraction -**
    I used all of the variables, performed clustering using 20 clusters (used trial and error). Ran the clustering multiple times with random seeding to verify the consistency of the clustering. The following figure to the left contains a scatter plot of the two variables with the hue of the response variable and the one to the right contains a scatter plot showing the clusters. I used PCA to be able to plot the results within two dimensions -

![20cluster_7](https://user-images.githubusercontent.com/11637437/29794356-8cf6ab6e-8bfc-11e7-8807-36ed5561638e.png)

### Overfitting

I also found out that if I overfit my model to a certain degree, it improves prediction of true positives without compromising too much on the accuracy on the test set. In my personal opinion, a certain degree of overfit is reasonable in the case. That being said, it is important for the model to be *consistent* and *generalizable*. Hence, **I ran simulations** to verify that the model is fairly robust. I performed random several train, test and validation splits on the data 15 times and changed the proportion of test data from 20% to 60% of the total available data. The results were consistent.

Following is the summary of my results of the "consistency test" -

![overfit_consistency](https://user-images.githubusercontent.com/11637437/29989526-6f7a60a6-8f28-11e7-91a1-1f2de7921696.PNG)

## Final Evaluation

Hence, here is my final model and the final results.

![result_final](https://user-images.githubusercontent.com/11637437/29794670-d5d0de62-8bfd-11e7-8cda-86f7795c5791.PNG)
