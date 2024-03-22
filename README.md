# Where'd My Power Go?
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
  src="assets/fin_uni.html"
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

### NMAR Analysis:
While exploring the dataset we came across a column that had seemingly random NA values. This column was the CAUSE.CATEGORY.DETAILS column. After closer inspection we had decided that the missing mechanism behind this column was NMAR. Our main line of reasoning is that if there are no details for a given cause/ or the details were too difficult to obtain then the value would be left empty. The significance of the details may be small and it might also be left out for that reason. This would then mean the missingness is NMAR as the missingness depends upon the column itself. However if we were to want to test this we would check to see it was MAR by comparing it to the original CAUSE.CATEGORY column.

### Missingness Dependency:
A key figure we want to find out is what the missingness mechanism of the Duration Minutes column is. If we find a suitable MAR relationship with our column then we may be able to properly impute the missing data. In our testing we wanted to look at the relationship between Duration Minutes and Population. If there's a smaller or large population does this lead to the missingness of the duration column? 

We first made a plot for the distribution of population when the duration column was missing and not missing. The distributions look about the same except for the one outlier under the 8 million population mark. This might be the key to showing the data is MAR.

<iframe
  src="assets/mness_plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
We then needed to complete a permutation test with our test statistic being the K-S statistic. We followed a pretty simple process, where we computed our observed K-S statistic given our original data and then permuted the NERC.REGION column and computed the K-S statistic once more. We permuted the data 500 times and stored each statistic. Below is the distribution of the permuted K-S statistics along with the red line being the observed statistic. 

<iframe
  src="assets/es_dist.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

From this we can conclude that, with a significance level of 0.05, we fail to reject that the Durations column missingness is dependent on population. Our p-value was just too high and this suggests that the relationship is elsewhere. Through more testing we found that the missingness of the Duration column actually depends on the categorical column of the NERC REGIONS.

---

## **Hypothesis Testing**
Previously we saw that there were some differences in the duration of an outage in regards to the region. Since most outages came from the WECC and RFC regions we wanted to see if one region had longer outage time than the other. To do this we conducted a permutation test.

### Null Hypothesis:
WECC region has identical power outage duration times to the RFC region

### Alternative Hypothesis:
WECC region has a greater power outage duration than those in the RFC region.

### Test Statistic:
Our test statistic will be the difference in outage duration means for both regions. Since we are using a permutation test we would normally use a statistic that described the difference in the distributions. However since we have the ability to be specific we are able to average the times of each group instead and use that difference as our statistic. It makes our test clear to understand. We chose a significance level of 0.05. There isn't a major reason for this significance level but it is low enough to take into account any small differences we find in our permutation test. After conducting our permutation test we took a look at our distribution of the difference in mean times between regions, shown below.


<iframe
  src="assets/hypothesis_fig.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
We calculated the p-value based off of the above distribution and got a value of 0.00.
Since this value is less than 0.05 we are able to reject the null hypothesis in favor of the alternative.


---

## **Framing a Prediction Problem**
Have you ever been playing Fortnite and the power suddenly goes out? Your immediate thought would be ‘when is this power coming back i have to get back to Fortnite!’. Trust us, we’ve all had these thoughts. Our prediction problem is a regression one and focuses on predicting the amount of time one has to wait till the power outage is over. The response variable will be the Duration Minutes column since this column was created manually and excludes any discrepancies within the given OUTAGE.DURATION column. For our metric we are using RMSE over R^2, seeing that our numbers are quite large and vary significantly the RMSE will give us an idea of how far off the model is and be interpretable.


---

## **Baseline Model**
Our model uses 5 features: The Cause Category of the event , the respective NERC region, the amount of power is selling for in a given month for the residential sector, and the respective residential/industrial customer percentage. The residential/ industrial customer percentage would be something that fluctuates if it were to be grabbed in the moment. Three numerical columns and two categorical columns. For the model we One Hot Encoded the two categorical columns.
After fitting the data and predicting values based on the training data and testing data our resulting RMSE values are surprising. The training RMSE (3669.477) is higher than our testing RMSE (3661.377) which is good but a little unexpected. Both RMSE values are above 3000 which seems high, but the response variable, duration, is measured in minutes. So this means that our model is roughly off by 2days, which is quite high given that most of our data points have
a duration of less than a day but not too bad when considering the much higher outage durations.
This means our current model doesn't work the best it could, seeing that our RMSE is still pretty high regardless of measurements and can definitely be improved.


---

## **Final Model**

For our final model, to improve accuracy we couldn’t introduce new quantitative features as we had already included features that had any resemblance of a linear relationship with outage duration. We instead focused on looking at these distributions once again and seeing what kind of transformations we can make in order to improve the RMSE of our model. What we believed is that since in each one of our quantitative distributions we have large clusters of data centered at low wait times we and some small clusters surrounding large wait times. We could quantize the data to account for the extremes and also make the data uniform. The goal at this point is to make our predictions smaller as it seems to be overshooting. Quantizing allows us to do so and we applied this transformation to all three quantitative features. The only real hyperparameter we can choose in this situation is the number of quantiles and we set it to the length of the dataset. This makes sense as our data is volatile and although most clusters have low times, in between those clusters are values that are abnormally high and so it is best to get the maximum number of quantiles. After running the new model on the same training and test data we saw a small but noticeable improvement. The training RMSE (3157.560) and testing RMSE (3208.462) are noticeably smaller than the original models RMSE. We improved the accuracy of our model by about 11%. 

---

## **Fairness Analysis**
For our fairness analysis we will have to look for groups not being used in our model such as Year.In this case we will look if our model is worse on the first half of the given years in the dataset (2000-2009) in comparison to the other half (2010 - 2016)
Our Hypothesis test is as follows:
Null: The model has identical RMSE for the first half of the years (2000-2009) and the second half (2010-2016)
Alternative: The model has a higher RMSE for the first half of years (2000-2009) compared to the second half (2010-2016)
We will run some permutation tests to test our hypothesis. The resulting distribution of RMSE differences between the two groups is shown below.


<iframe
  src="assets/fairness_plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
With a significance value of 0.05 and an obtained p-value of 0.00 we are able to reject the null in favor of the alternative. This means that our model does perform worse in earlier years which is an area we would need to improve. This may be due to multiple reasons, one of which being that we did not take into account inflation when looking at the RES.SALES column. Another might be that the severity of natural disasters might have worsened as a result of global warming. Nonetheless our model is not fair to these two groups and would need to be taken into account.

--- 

## References

https://www.sciencedirect.com/science/article/pii/S2352340918307182
https://engineering.purdue.edu/LASCI/research-data/outages
