# Power Outage Data Analysis Report
by Jessica Zhang and Tongxun Hu

# Introduction

Are the main causes of power outages under cold climates the same as
the main causes of power outages under warm climates? 
In other words, is the distribution of the causes of power outages
the same under cold climates and warm climates?

------
# Data Cleaning and EDA

**Data Cleaning**

newnewnew

**Univariate Analysis**

**Bivariate Analysis**

**Interesting Aggregates**

------
# Assessment of Missingness

**NMAR Analysis**

**Missingness Dependency**

------
# Hypothesis Testing

<!-- <iframe src="assets/03-eda.html" width=800 height=600 frameBorder=0></iframe> -->

|   YEAR |   MONTH | U.S._STATE   | POSTAL.CODE   | CLIMATE.REGION     | CLIMATE.CATEGORY   | OUTAGE.START.DATE         | OUTAGE.START.TIME   | OUTAGE.RESTORATION.DATE    | OUTAGE.RESTORATION.TIME   | CAUSE.CATEGORY     | CAUSE.CATEGORY.DETAIL   |   HURRICANE.NAMES |   OUTAGE.DURATION |   DEMAND.LOSS.MW |   CUSTOMERS.AFFECTED |   TOTAL.CUSTOMERS | OUTAGE.START        | OUTAGE.RESTORATION   |   CUSTOMERS.PERCENTAGE |
|-------:|--------:|:-------------|:--------------|:-------------------|:-------------------|:--------------------------|:--------------------|:---------------------------|:--------------------------|:-------------------|:------------------------|------------------:|------------------:|-----------------:|---------------------:|------------------:|:--------------------|:---------------------|-----------------------:|
|   2011 |       7 | Minnesota    | MN            | East North Central | normal             | Friday, July 1, 2011      | 5:00:00 PM          | Sunday, July 3, 2011       | 8:00:00 PM                | severe weather     | nan                     |               nan |              3060 |              nan |                70000 |           2595696 | 2011-07-01 17:00:00 | 2011-07-03 20:00:00  |                2.69677 |
|   2014 |       5 | Minnesota    | MN            | East North Central | normal             | Sunday, May 11, 2014      | 6:38:00 PM          | Sunday, May 11, 2014       | 6:39:00 PM                | intentional attack | vandalism               |               nan |                 1 |              nan |                  nan |           2640737 | 2014-05-11 18:38:00 | 2014-05-11 18:39:00  |              nan       |
|   2010 |      10 | Minnesota    | MN            | East North Central | cold               | Tuesday, October 26, 2010 | 8:00:00 PM          | Thursday, October 28, 2010 | 10:00:00 PM               | severe weather     | heavy wind              |               nan |              3000 |              nan |                70000 |           2586905 | 2010-10-26 20:00:00 | 2010-10-28 22:00:00  |                2.70594 |
|   2012 |       6 | Minnesota    | MN            | East North Central | normal             | Tuesday, June 19, 2012    | 4:30:00 AM          | Wednesday, June 20, 2012   | 11:00:00 PM               | severe weather     | thunderstorm            |               nan |              2550 |              nan |                68200 |           2606813 | 2012-06-19 04:30:00 | 2012-06-20 23:00:00  |                2.61622 |
|   2015 |       7 | Minnesota    | MN            | East North Central | warm               | Saturday, July 18, 2015   | 2:00:00 AM          | Sunday, July 19, 2015      | 7:00:00 AM                | severe weather     | nan                     |               nan |              1740 |              250 |               250000 |           2673531 | 2015-07-18 02:00:00 | 2015-07-19 07:00:00  |                9.35093 |