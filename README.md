# Power Outage Project
by Marcus Ruesga (mruesga@ucsd.edu) and Angel Hernandez (anh048@ucsd.edu)

***Note***: If you choose a repo name and title as uninspired as the ones here, I will be quite sad.

---

## Introduction



---

## **Data Cleaning and Exploratory Data Analysis**

### Data Cleaning
Describe, in detail, the data cleaning steps you took and how they affected your analyses. The steps should be explained in reference to the data generating process. Show the head of your cleaned DataFrame (see Part 2: Report for instructions).


|   Residential Sales | NERC.REGION   |   Residential Percentage |   POPULATION | CAUSE.CATEGORY     |   CUSTOMERS.AFFECTED |   Residential Customer Percentage |   IND.CUST.PCT |   YEAR | Start Time          | End Time            |   Year | Duration        |   Duration Minutes |
|--------------------:|:--------------|-------------------------:|-------------:|:-------------------|---------------------:|----------------------------------:|---------------:|-------:|:--------------------|:--------------------|-------:|:----------------|-------------------:|
|             38881.9 | MRO           |                  35.5491 |      5348119 | severe weather     |                70000 |                           88.9448 |       0.411181 |   2011 | 2011-07-01 17:00:00 | 2011-07-03 20:00:00 |   2011 | 2 days 03:00:00 |               3060 |
|             26449.8 | MRO           |                  30.0325 |      5457125 | intentional attack |                  nan |                           88.8335 |       0.37482  |   2014 | 2014-05-11 18:38:00 | 2014-05-11 18:39:00 |   2014 | 0 days 00:01:00 |                  1 |
|             24454.9 | MRO           |                  28.0977 |      5310903 | severe weather     |                70000 |                           88.9206 |       0.392361 |   2010 | 2010-10-26 20:00:00 | 2010-10-28 22:00:00 |   2010 | 2 days 02:00:00 |               3000 |
|             30858.7 | MRO           |                  31.9941 |      5380443 | severe weather     |                68200 |                           88.8954 |       0.422355 |   2012 | 2012-06-19 04:30:00 | 2012-06-20 23:00:00 |   2012 | 1 days 18:30:00 |               2550 |
|             33814.6 | MRO           |                  33.9826 |      5489594 | severe weather     |               250000 |                           88.8216 |       0.367005 |   2015 | 2015-07-18 02:00:00 | 2015-07-19 07:00:00 |   2015 | 1 days 05:00:00 |               1740 |

### Univariate Analysis
<iframe
  src="assets/plot_test.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
Embed at least one plotly plot you created in your notebook that displays the distribution of a single column (see Part 2: Report for instructions). Include a 1-2 sentence explanation about your plot, making sure to describe and interpret any trends present. (Your notebook will likely have more visualizations than your website, and that’s fine. Feel free to embed more than one univariate visualization in your website if you’d like, but make sure that each embedded plot is accompanied by a description.)

### Bivariate Analysis
<iframe
  src="assets/final_bivar_plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
Embed at least one plotly plot that displays the relationship between two columns. Include a 1-2 sentence explanation about your plot, making sure to describe and interpret any trends present. (Your notebook will likely have more visualizations than your website, and that’s fine. Feel free to embed more than one bivariate visualization in your website if you’d like, but make sure that each embedded plot is accompanied by a description.)

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

Embed at least one grouped table or pivot table in your website and explain its significance.

---

## **Assessment of Missingness**
<iframe
  src="assets/missing_plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/notmissing_plot.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/huh.html"
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

Clearly state your choice of Group X and Group Y, your evaluation metric, your null and alternative hypotheses, your choice of test statistic and significance level, the resulting 
p
-value, and your conclusion.

Optional: Embed a visualization related to your permutation test in your website.