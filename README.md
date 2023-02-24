# Power Outage Data Analysis Report
by Jessica Zhang and Tongxun Hu

# Introduction

This data analysis report uses power outage dataset as the main source. This dataset includes the major power outage data in the continental U.S. from January 2000 to July 2016. 
The question that we are going to investigate is: Are the main causes of power outages under cold climates the same as
the main causes of power outages under warm climates? 

The question and the information on the dataset is significant because it could be used to identify and analyze the patterns and characteristics of major power outages in the U.S., and therefore assess the risk predictors more accurately and better prepare for the future power outage.

The original dataset contains 1540 rows and 57 columns. After brief cleaning and dropping irrelevant columns, the dataset we mainly work on has 1534 rows and 16 columns. 

Below are the relevant columns and their explanations:
- YEAR: Indicates the year when the outage event occurred
- MONTH : Indicates the month when the outage event occurred
- U.S._STATE : Represents all the states in the continental U.S.
- POSTAL.CODE : Represents the postal code of the U.S. states
- CLIMATE.REGION : U.S. Climate regions as specified by National Centers for Environmental Information (nine climatically consistent regions in continental U.S.A.)
- CLIMATE.CATEGORY : This represents the climate episodes corresponding to the years. The categories—“Warm”, “Cold” or “Normal” episodes of the climate are based on a threshold of ± 0.5 °C for the Oceanic Niño Index (ONI)
- OUTAGE.START.DATE : This variable indicates the day of the year when the outage event started
- OUTAGE.START.TIME : This variable indicates the time of the day when the outage event started
- OUTAGE.RESTORATION.DATE : This variable indicates the day of the year when power was restored to all the customers
- OUTAGE.RESTORATION.TIME : This variable indicates the time of the day when power was restored to all the customers
- CAUSE.CATEGORY : Categories of all the events causing the major power outages
- HURRICANE.NAMES: If the outage is due to a hurricane, then the hurricane name is given by this variable
- OUTAGE.DURATION: Duration of outage events (in minutes)
- CUSTOMERS.AFFECTED : Number of customers affected by the power outage event
- TOTAL.CUSTOMERS : Annual number of total customers served in the U.S. state


------
# Data Cleaning and EDA

**Data Cleaning**

After loading in the data from the csv file, we found that the first four rows were all nan values due to the formatting error, so we dropped these rows. Then we replaced the column names with the original column names in the fifth row, and added the units (located at the sixth row) to the column names. In addition, we dropped many irrelevant columns after carefully reviewing all of them. Moreover, we combined OUTAGE.START.DATE with OUTAGE.START.TIME and OUTAGE.RESTORATION.DATE and OUTAGE.RESTORATION.TIME to get two new columns with Timestamp values (OUTAGE.START and OUTAGE.RESTORATION), while leaving nan as it is. Lastly, since columns that should be numeric are stored as strings, we used pd.to_numeric to change the columns with nan values from string to float, and used astype for those without nan values. 

Below is the head of the cleaned dataframe:

`print(outage.head().to_markdown(index=False))`

|   YEAR |   MONTH | U.S._STATE   | POSTAL.CODE   | CLIMATE.REGION     | CLIMATE.CATEGORY   | OUTAGE.START.DATE         | OUTAGE.START.TIME   | OUTAGE.RESTORATION.DATE    | OUTAGE.RESTORATION.TIME   | CAUSE.CATEGORY     | CAUSE.CATEGORY.DETAIL   |   HURRICANE.NAMES |   OUTAGE.DURATION |   DEMAND.LOSS.MW |   CUSTOMERS.AFFECTED |   TOTAL.CUSTOMERS | OUTAGE.START        | OUTAGE.RESTORATION   |   CUSTOMERS.PERCENTAGE |
|-------:|--------:|:-------------|:--------------|:-------------------|:-------------------|:--------------------------|:--------------------|:---------------------------|:--------------------------|:-------------------|:------------------------|------------------:|------------------:|-----------------:|---------------------:|------------------:|:--------------------|:---------------------|-----------------------:|
|   2011 |       7 | Minnesota    | MN            | East North Central | normal             | Friday, July 1, 2011      | 5:00:00 PM          | Sunday, July 3, 2011       | 8:00:00 PM                | severe weather     | nan                     |               nan |              3060 |              nan |                70000 |           2595696 | 2011-07-01 17:00:00 | 2011-07-03 20:00:00  |                2.69677 |
|   2014 |       5 | Minnesota    | MN            | East North Central | normal             | Sunday, May 11, 2014      | 6:38:00 PM          | Sunday, May 11, 2014       | 6:39:00 PM                | intentional attack | vandalism               |               nan |                 1 |              nan |                  nan |           2640737 | 2014-05-11 18:38:00 | 2014-05-11 18:39:00  |              nan       |
|   2010 |      10 | Minnesota    | MN            | East North Central | cold               | Tuesday, October 26, 2010 | 8:00:00 PM          | Thursday, October 28, 2010 | 10:00:00 PM               | severe weather     | heavy wind              |               nan |              3000 |              nan |                70000 |           2586905 | 2010-10-26 20:00:00 | 2010-10-28 22:00:00  |                2.70594 |
|   2012 |       6 | Minnesota    | MN            | East North Central | normal             | Tuesday, June 19, 2012    | 4:30:00 AM          | Wednesday, June 20, 2012   | 11:00:00 PM               | severe weather     | thunderstorm            |               nan |              2550 |              nan |                68200 |           2606813 | 2012-06-19 04:30:00 | 2012-06-20 23:00:00  |                2.61622 |
|   2015 |       7 | Minnesota    | MN            | East North Central | warm               | Saturday, July 18, 2015   | 2:00:00 AM          | Sunday, July 19, 2015      | 7:00:00 AM                | severe weather     | nan                     |               nan |              1740 |              250 |               250000 |           2673531 | 2015-07-18 02:00:00 | 2015-07-19 07:00:00  |                9.35093 |

**Univariate Analysis**

<iframe src="assets/cause.html" width=800 height=600 frameBorder=0></iframe>

This is the histogram of distribution/percentage of the causes of power outages(CAUSE.CATEGORY). From the graph, we can see that the number one cause of major power outage is severe weather, the second one is intentional attack, and the last one is islanding. 

**Bivariate Analysis**

<iframe src="assets/climate_cause.html" width=800 height=600 frameBorder=0></iframe>

This is the grouped bar chart between climate and causes. It shows the percentage of each climate in different causes. From the graph, we can see that in every kind of causes, the normal climate has the biggest percentage, followed by the cold climate, and warm climate has relatively the smallest percentage in all causes.

**Interesting Aggregates**

`print(pivot.to_markdown())`

| CAUSE.CATEGORY                |   cold |   normal |   warm |
|:------------------------------|-------:|---------:|-------:|
| equipment failure             |     19 |       28 |     10 |
| fuel supply emergency         |     19 |       26 |      5 |
| intentional attack            |    122 |      226 |     70 |
| islanding                     |     15 |       17 |     14 |
| public appeal                 |     22 |       34 |     13 |
| severe weather                |    239 |      354 |    166 |
| system operability disruption |     37 |       59 |     30 |


This is a pivot table describing the joint distribution of climate and causes, which is closely related to the question. This pivot table is very helpful since it clearly shows us the distributions of each combination and gives us a sense of what our hypothesis test is going to look like and how should we approach it. 

------
# Assessment of Missingness

**NMAR Analysis**



**Missingness Dependency**

The column we choose to focus on that contains missingness is the column CUSTOMERS.AFFECTED. 

The first question that we are going to raise is whether the missingness of CUSTOMER.AFFECTED column depends on CAUSE.CATEGORY column. 
The null hypothesis is that the distribution of causes of outages when affected_customers is missing is the same as the distribution of causes of outages when affected_customers is not missing.
The alternative hypothesis is that the two distributions are different.
After performing the permutation test, we have found that the resulting p-value is 0.0, so we reject the null hypothesis. Therefore, we come to the conclusion that the missingness in the affected_customers column is dependent on causes of power outages.

The second question that we propose is whether the missingness of CUSTOMER.AFFECTED column depends on TOTAL.CUSTOMERS column.
The null hypothesis is that the distribution of total customers when affected_customers is missing is the same as the distribution of total customers when affected_customers is not missing.
The alternative hypothesis is that the two distributions are different.
After doing the permutation test, we have found that the p-value is 0.802. Therefore, we fail to reject the null hypothesis and conclude that the missingness in the affected_customers column is not dependent on total customers.

<iframe src="assets/kde.html" width=800 height=600 frameBorder=0></iframe>

The above graph shows that the two distributions have similar shape, but are centered at different values, so they might not belong to the same population.

------
# Hypothesis Testing

