# Power Outage Project
by Angel Hernandez (anh048@ucsd.edu) Marcus Ruesga (mruesga@ucsd.edu)


---

## Introduction

The dataset "Major Power Outage Rankings in the U.S." originates from the "Laboratory for Advancing Sustainable Critical Infrastructure" at Purdue University. This dataset received its information from publicly available datasets such as : (i) OE-417 form Schedule 1 published by DOE׳s Office of Electricity Delivery and Energy Reliability [2] (ii) U.S. Energy Information Administration (EIA) [form EIA-826 and EIA-861] [3]; (iii) National Oceanic and Atmospheric Administration (NOAA) and National Climatic Data Center (NCDC) [4]; (iv) U.S. Department of Labor; Bureau of Labor Statistics [5]; (v) U.S. Census Bureau.

The original dataset includes the major outages witnessed by different states in the continental U.S. between January 2000 and July 2016 and contains 1534 observations(1533 rows) and 55 features related to the major outage patterns. Some of the features used to describe the observations of these major power outages include indications of the location, time, cause, electricity consumption, and economic descriptions related to these outage events.

There are many factors for why power outages occur, but the question we raise is: Why do certain power outages take longer in comparison to others?

It's valuable for people to understand why some power outages take longer than others, so we as a society can discover whether or not it’s an issue we can resolve, or if it's an issue beyond our reach. There are  several factors to consider when determining what causes outages to take so long, such as weather, location, resource availability, accessibility, and the extent of the damages.

After examining the original dataset we discovered there are many features that were not necessary to help us answer our question. After filtering the dataset, our relevant dataset contained  1534 observations(1533rows) and 12 features. The features that were relevant to why some power outages take longer were RES.SALES, NERC.REGION, RES.PERCEN, POPULATION, CAUSE.CATEGORY, CUSTOMERS.AFFECTED, OUTAGE.START.TIME, OUTAGE.RESTORATION.TIME, YEAR, CUSTOMERS.AFFECTED, RES.CUST.PCT, and IND.CUST.PCT.


|Column	                 |Description|
|---                     |---        |
|`'RES.SALES'`              |Electricity consumption in the residential sector (megawatt-hour)|
|`'NERC.REGION'`             |The North American Electric Reliability Corporation (NERC) regions involved in the outage event|
|`'RES.PERCEN'` |Percentage of residential electricity consumption compared to the total electricity consumption in the state (in %)|
|`'POPULATION'`     |Population in the U.S. state in a year|
|`'CAUSE.CATEGORY'` |Categories of all the events causing the major power outages|
|`'CUSTOMERS.AFFECTED'`       |Number of customers affected by the power outage event|
|`'RES.CUST.PCT'`         |Percent of residential customers served in the U.S. state (in %)|
|`'IND.CUST.PCT'`         |Percent of industrial customers served in the U.S. state (in %)|
|`'YEAR'`         |Indicates the year when the outage event occurred|
|`'OUTAGE.START.TIME'`       |This variable indicates the time of the day when the outage event started (as reported by the corresponding Utility in the region)|
|`'OUTAGE.START.DATE'`       |This variable indicates the day of the year when the outage event started (as reported by the corresponding Utility in the region)|
|`'OUTAGE.RESTORATION.DATE'`       |This variable indicates the day of the year when power was restored to all the customers (as reported by the corresponding Utility in the region)|
|`'OUTAGE.RESTORATION.TIME'`       |This variable indicates the time of the day when power was restored to all the customers (as reported by the corresponding Utility in the region)|

---

## **Data Cleaning and Exploratory Data Analysis**

### Data Cleaning
Our data cleaning started with exploring each column first. With NERC.REGION we noticed that some regions represented the same region with a different name, this was mainly shown through hawaii. We changed the similar names down to the nationally recognized one. We then looked at the restoration and start times / dates columns and combined them respectively and created a uniform datetime column for the start and restoration times. For a measure of accuracy we then created our own Duration Minutes column which took the difference in the datetime columns and stored that difference in minutes. This was our initial set of data cleaning as in data analysis we discovered more factors that would help us clean our data better.


|   Residential Sales | NERC.REGION   |   Residential Percentage |   POPULATION | CAUSE.CATEGORY     |   CUSTOMERS.AFFECTED |   Residential Customer Percentage |   IND.CUST.PCT |   YEAR | Start Time          | End Time            |   Year | Duration        |   Duration Minutes |
|--------------------:|:--------------|-------------------------:|-------------:|:-------------------|---------------------:|----------------------------------:|---------------:|-------:|:--------------------|:--------------------|-------:|:----------------|-------------------:|
|             38881.9 | MRO           |                  35.5491 |      5348119 | severe weather     |                70000 |                           88.9448 |       0.411181 |   2011 | 2011-07-01 17:00:00 | 2011-07-03 20:00:00 |   2011 | 2 days 03:00:00 |               3060 |
|             26449.8 | MRO           |                  30.0325 |      5457125 | intentional attack |                  nan |                           88.8335 |       0.37482  |   2014 | 2014-05-11 18:38:00 | 2014-05-11 18:39:00 |   2014 | 0 days 00:01:00 |                  1 |
|             24454.9 | MRO           |                  28.0977 |      5310903 | severe weather     |                70000 |                           88.9206 |       0.392361 |   2010 | 2010-10-26 20:00:00 | 2010-10-28 22:00:00 |   2010 | 2 days 02:00:00 |               3000 |
|             30858.7 | MRO           |                  31.9941 |      5380443 | severe weather     |                68200 |                           88.8954 |       0.422355 |   2012 | 2012-06-19 04:30:00 | 2012-06-20 23:00:00 |   2012 | 1 days 18:30:00 |               2550 |
|             33814.6 | MRO           |                  33.9826 |      5489594 | severe weather     |               250000 |                           88.8216 |       0.367005 |   2015 | 2015-07-18 02:00:00 | 2015-07-19 07:00:00 |   2015 | 1 days 05:00:00 |               1740 |

### Univariate Analysis

The main thing we are concerned about is the distribution of the wait times, so looking at this alone we see that most wait times are less than 1000 minutes,  however we originally noticed extremely high times. After some research we found that the longest power outage within 2000-2016 was no longer than two weeks (24000 minutes). We are going to assume that the data points with times higher than two weeks are faulty and we chose to ignore these data points by dropping them. The resulting distribution of the new times are shown below.

<iframe
  src="assets/plot_test.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


### Bivariate Analysis

<iframe
  src="assets/final_bivar_plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
This plots RES.SALES against Duration Minutes. We can see there isn't a clear relationship between the two however there is a strong clustering of low wait times when sales are low in comparison to high sales.

### Interesting Aggregates

| NERC.REGION   |   Duration Minutes |   Residential Sales |
|:--------------|-------------------:|--------------------:|
| ECAR          |            5603.31 |            52080.5  |
| FRCC          |            4182.5  |           169785    |
| RFC           |            2937.92 |            50475.4  |
| MRO           |            2934.95 |            27110    |
| NPCC          |            2711.3  |            40712.9  |
| SPP           |            2693.77 |            57476.5  |
| TRE           |            2493.26 |           194092    |
| SERC          |            1601.04 |            62746.5  |
| WECC          |            1061.04 |            77537.3  |
| HECO          |             845.4  |             4392.29 |

For this table we wanted to see any significance in the NERC.REGION in regards to some of our quantitative columns. We first grouped the NERC.REGION then chose the Duration Minutes and RES.SALES column. We aggregated these columns using the mean. With the resulting table we see the certain regions have a significantly higher outage time, possible due to that area experiencing more natural disasters. In regard to the sales columns, this pretty much outlines which regions make the most revenue and this also plays a part in that region's population. 

---

## **Assessment of Missingness**

<iframe
  src="assets/mness_plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/es_dist.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
State whether you believe there is a column in your dataset that is NMAR. Explain your reasoning and any additional data you might want to obtain that could explain the missingness (thereby making it MAR). Make sure to explicitly use the term “NMAR.”

Present and interpret the results of your missingness permutation tests with respect to your data and question. Embed a plotly plot related to your missingness exploration; ideas include:
• The distribution of column 
Y
 when column 
X
 is missing and the distribution of column 
Y
 when column 
X
 is not missing, as was done in Lecture 8.
• The empirical distribution of the test statistic used in one of your permutation tests, along with the observed statistic.

---

## **Hypothesis Testing**

Clearly state your null and alternative hypotheses, your choice of test statistic and significance level, the resulting 
p
-value, and your conclusion. Justify why these choices are good choices for answering the question you are trying to answer.

Optional: Embed a visualization related to your hypothesis test in your website.

Tip: When making writing your conclusions to the statistical tests in this project, never use language that implies an absolute conclusion; since we are performing statistical tests and not randomized controlled trials, we cannot prove that either hypothesis is 100% true or false.

### Null Hypothesis

### Alternative Hypothesis

<iframe
  src="assets/hypothesis_fig.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

---

## **Framing a Prediction Problem**

Clearly state your prediction problem and type (classification or regression). If you are building a classifier, make sure to state whether you are performing binary classification or multiclass classification. Report the response variable (i.e. the variable you are predicting) and why you chose it, the metric you are using to evaluate your model and why you chose it over other suitable metrics (e.g. accuracy vs. F1-score).

Note: Make sure to justify what information you would know at the “time of prediction” and to only train your model using those features. For instance, if we wanted to predict your final exam grade, we couldn’t use your Project 4 grade, because Project 4 is only due after the final exam! Feel free to ask questions if you’re not sure.

---

## **Baseline Model**

Describe your model and state the features in your model, including how many are quantitative, ordinal, and nominal, and how you performed any necessary encodings. Report the performance of your model and whether or not you believe your current model is “good” and why.

Tip: Make sure to hit all of the points above: many projects in the past have lost points for not doing so.

---

## **Final Model**

State the features you added and why they are good for the data and prediction task. Note that you can’t simply state “these features improved my accuracy”, since you’d need to choose these features and fit a model before noticing that – instead, talk about why you believe these features improved your model’s performance from the perspective of the data generating process.

Describe the modeling algorithm you chose, the hyperparameters that ended up performing the best, and the method you used to select hyperparameters and your overall model. Describe how your Final Model’s performance is an improvement over your Baseline Model’s performance.

Optional: Include a visualization that describes your model’s performance, e.g. a confusion matrix, if applicable.

---

## **Fairness Analysis**

<iframe
  src="assets/fairness_plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
Clearly state your choice of Group X and Group Y, your evaluation metric, your null and alternative hypotheses, your choice of test statistic and significance level, the resulting 
p
-value, and your conclusion.

Optional: Embed a visualization related to your permutation test in your website.