---
title: "Averages"
layout: page
---

Many key product metrics are averages - _average_ revenue per user, _average_ time on site, and so on. There are different kinds of average, but all seek to find a typical or representative value for a dataset. In order to understand how well an average does this it is also important to know how the datapoints are _distributed_. 


## Mean and Median

The most familiar kind of average involves adding a set of numbers together and dividing the result by the size of the set. This is the **mean average** - in Excel or Google Sheets this is what the `AVERAGE` function does.

For example imagine running an e-commerce product for which we want to track the average shopping cart size. In theory this is quite simple - add up the order value for each transaction in a given period and divide it by the number of transactions:

```{.math}
Transactions: $5, $25, $8, $50, $32, $7, $5, $100, $9, $10, $18, $61, $5, $12, $7, $9, $14, $40, $6, $30

Total = $453 

Average cart size = $453/20 = $23
```

As a simple metric we could optimise the product around (and with a more realistic amount of data) this might work pretty well. However we can see that there are ten orders of ten dollars or less, seven between $10 and $50 and one jumbo order of $100. So it may be misleading to say that $23 represents a typical cart size. Alternatively, we might take the **median** value, which is obtained by lining all the datapoints up and taking the middle one (if an odd number of datapoints) or the average of the two middle ones (if an even number of datapoints)

```{.math}
$5 $5 $5 $6 $7 $7 $8 $9 $9 [$10 $12] $14 $18 $25 $30 $32 $40 $52 $61 $100

Median cart size = $10+$12/2 = $11
```

Median averages are less sensitive to distortion by outliers, and are often used when a dataset contains a large number of smaller values and a small number of very high values, like the income data for a country. If that $100 order were replaced by one of $1000 then the mean order size would shoot up to $68, while the median remained at $11.

A third kind of average is the **mode**, which is the most common value in a dataset. In this case it would be $5. Modes are seldom used to summarise numerical data of this kind, but they are the only kind of average you can apply to categorical data like gender or names of countries. 

## Distribution

In this contrived example it isn't really obvious whether the mean or the median is most useful. It would be useful if we were able to picture the **distibution** of points in the dataset. 

We can do this by making a *frequency table* which groups the datapoints into buckets or *bins*: 

|Order size|Number of orders|
|-|-|
|$0-$9|9|
|$10-$24|4|
|$25-$49|4|
|$50-$99|2|
|$100 or more|1|

This can be visualised as a *histogram* or *bar chart* ^[There are important technical distinctions between these two kind of charts, but they're not easy to respect using spreadsheet tools or really important in this context]:

![](/assets/images/fig2-1.png)

Examining the dataset in this way might help identify a segmentation strategy to look for the differences between the low and high value orders, and how to convert one to the other. 

Unfortunately when dealing with digital products we often don't have access to the underlying dataset. We're rarely able to access the raw data for each individual session recorded in an analytics tool, and instead see canned averages produced by the tool like *average session duration* or *average pages per visit*. These numbers are not always straightforward to calculate and may make poor key performance metrics. Some tools are able to produce histograms which indicate the underlying distribution of this kind of data, like these examples from Google Analytics:

![](/assets/images/fig2-2.png)

When we're unsure what to do with an unfamiliar dataset then a common first instinct is to take the average of it. It would be far better to get some idea of the overall distribution and shape of the dataset first, and a number of tools are available to make this easier. 

## Summarising Data Sidebar

The statistical programming language **R** has a `summary()` function which produces results like this:

```R
summary(x)
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
   5.00    7.00   11.00   22.65   30.50  100.00 
```

Where the dataset `x` is the shopping cart example from above. You can see this gives us the mean and the median, as well as the largest and smallest values in the dataset and the values representing the upper and lower quartiles. R also has a simple function for plotting a [histogram](https://www.r-bloggers.com/how-to-make-a-histogram-with-basic-r/):

```R
hist(x)
```

Excel has standard functions for `AVERAGE`, `MEDIAN`, `MAX`, `MIN` and `QUARTILE`, as do Google Sheets and Apple Numbers. Excel's *Data Analysis* [add-on](https://support.office.com/en-ie/article/load-the-analysis-toolpak-in-excel-6a63e598-cd6d-42e3-9317-6b40ba1a66b4) provides a 'Descriptive Statistics' feature which will yield all this and more, while Google Sheets offers a neat function to plot a basic histogram automatically. 