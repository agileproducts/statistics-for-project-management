---
title: "Sampling and Confidence Intervals"
layout: page
mathjax: true
---

Digital products generate a lot of data. It isn't always practical to measure each individual event interaction. Often we are dealing with a *sample* of data, from a certain fraction of users, or for an arbitary time window. The process of sampling introduces a degree of uncertainty into a measurement, but statistics allow us to quantify this uncertainty. 

## Simple random sampling

We have a button on a web page, and we want to know what proportion of visitors click on it, which we might call the **conversion rate** for the goal of clicking the button. 

```{.math}
conversion rate = number of button clicks / number of visitors
```

Let's say we had 10,000 visitors and 984 of them clicked the button. That's a conversion rate of 9.84%. We will ignore here the complication of whether a given visitor viewed the same page more than once and assume they did not. As a one-off measurement this is fine. If 10,000 people visited this page in the entire time it existed then we could say that 9.84% of visitors clicked the button. If 10,000 people visited in March then we could say that the conversion rate for March was 9.84%. 

However this is not how these kind of measurements usually work. Usually when we make this type of measurement we are looking at a **sample** of visitors and using the result to **infer** something about the wider population. We will use the conversion rate from 10,000 vistors to predict the number of conversions we will have from 100,000 visitors, or the rate we get today to predict what we will have tomorrow. Any kind of split testing by definition involves samples. Choosing individuals at random from a larger population is called [simple random sampling](https://en.wikipedia.org/wiki/Simple_random_sample). 

If we have measured that 984 visitors out of a sample of 10,000 clicked a button, can we really say that exactly 984 out of the next 10,000 will click it? Or that if we had randomly selected a different sample, we would get exactly the same result? It seems unlikely. Unfortunately that is what our reporting the conversion rate as 9.84% implies. It means 984 out of 10,000, not 983 or 985. This is another case of unjustified precision. 

## The probability of a result

Asking how likely it is that we will see 984 clicks in a sample of 10,000 is a question of **probability**. If we toss a two-sided coin, we know that the probability of getting heads is 50%. If we toss it twice then we know that we will most often get a head and a tail, but might well get two heads or two tails. If we toss it 10,000 times then we probably wouldn't get exactly 5000 heads, but we would expect to get a number fairly close to that and be astonished (and suspicious) if we got only 2500 heads. The probability of getting a particular number of heads from a particular number of coin tosses can be illustrated using the **binomial distribution**, so-called because the toss is a 'binary' event, with two possible outcomes from each 'trial'. 

![](/assets/images/fig3-1.png)

Most basic measurements of things like conversions on a website are of this type - a binary event with a yes/no outcome. Clicked the button, did not click the button. They can therefore be modelled using the binomial distibution. Actually, this is really the so-called *[normal approximation](https://en.wikipedia.org/wiki/Binomial_distribution#Normal_approximation)* to the binomial distibution, which states that for any sufficiently large number of trials the shape of the probability curve resembles the familiar 'bell curve' of the **[normal distribution](https://en.wikipedia.org/wiki/Normal_distribution)** . 'Sufficently large' being at least 5 trials, which any test in a digital environment will pass with ease [cite]. 

From the probability distribution, we can see that if the real probability of something happening is 9.84%, 0.0984 then seeing it happen 984 times in 10,000 trials is the single most likely outcome, but not that likely - there's only a little over 1% chance of getting that. There's a good chance of getting a number fairly close to that, and only a small chance of seeing it happen 920 or 1050 times. In fact this is really the wrong way around to think about it. We don't generally know the 'real' probability of something, that's what we are trying to work out, based on seeing a given number of successes in a given number of trials. If we see 984 clicks out of 10,000 visitors, the underlying conversion rate for the whole population is likely to be something close to 9.84%. But how close?

## Confidence intervals for a proportion

By calculating the area under the probability curve we can determine that if the probability of something happening is 9.84% then there's a 95% chance that if we will see between 926 and 1042 successes in 10,0000 trials. If we observe 984 button-clicks from a sample of 10,000 visitors we can say that it is 95% probable that the conversion rate for the entire population is between 9.26 and 10.42%. 

The spread of values from 926 to 1042 represents a **confidence interval**, the range either side of our sampled measurement in which, based on this data, the ‘real’ value for the whole population might lie. The width of this range was determined by the **confidence level** were were seeking, in this case 95%. Using this commonly accepted standard, if we took twenty samples then 19 times out of 20 the confidence interval attached to a sampled measurement would cover the true whole population value.

![](/assets/images/fig3-2.png)

The **confidence interval for a proportion** can be calculated as follows (<sup>1</sup>):


$$CI=\hat{p} \pm Z \sqrt{\frac{(\hat{p}(1-\hat{p})}{n}}$$


Where $n$ is the sample size or number of trials and $\hat{p}$ is the measurement. $Z$ is the [Z-score](../chapter-100/index.html#z-score) of the boundaries of interval required to deliver the desired confidence level. Z-scores for commonly used confidence levels are:


| Confidence Level  | Z |
| ------------- | ------------- |
| 99%   | 2.58  |
| 95%   | 1.96  |
| 90%   | 1.69  |
| 80%   | 1.28  |
   


For our example, at a confidence level of 95%:

$$
CI=0.0984 \pm 1.96 \sqrt{\frac{(0.0984(1-0.0984)}{10000}} \\~\\
 = 0.0984 \pm 0.0058  \\~\\
 = 0.0926~to~0.1042  \\~\\
$$

This is a pretty simple piece of maths to do in a spreadsheet:

||A|B|
|-|:-:|:-:|
|**1**|p|`measured conversion rate`|
|**2**|n|`sample size`|
|**3**|Z|`Z-score for desired confidence`|
|**4**|Half-Interval|`=B$3*SQRT((B$1*(1-B$1))/B$2)`|
|**5**|Lower Bound|`=B$1-B$4`|
|**6**|Lower Bound|`=B$1+B$4`|

It's worth reflecting on what this implies for the precision implied by those two decimal places in 9.84%. Were we to quote that as a single number it would suggest that our confidence interval was no wider than 9.835% to 9.845%. Rearranging the formula above and plugging in an interval of 0.005% (0.00005) yields a value for the sample size n of something like 100 million.  

In this example I would disregard that second decimal place of the percentage, given that we have a CI of ten times that width. Quoting the conversion rate as `9.8% +/- 0.6%` wouldn't be quite symmetrical rounding, but it's close enough. 

## Confidence intervals for a mean

If we taking a sample in order to measure the mean average of something then the formula for a confidence interval is slightly different (<sup>1</sup>, <sup>2</sup>). Here:

$$CI=\bar{x} \pm \sqrt{\frac{\sigma^2}{n}}$$

Where $\bar{x}$ is the mean of the sample, $n$ is again the sample size and $\sigma^2$ is the **variance** of the _population_. However if the sample size is sufficiently large (n>30) we can substitite the variance of the sample itself $s^2$ which can be calculated as:

$$s^2 = \frac{\sum_{i=1}^n (x_{i}-\bar{x})^2}{n-1}$$

Where $x_{i}$ is the value of each each datapoint in the sample. Fortunately spreadsheet tools have a built in `VAR()` function which does this for us, so we can perform the calculation like this:

||A|B|C|
|-|:-:|:-:|:-:|
|**1**|x~1~|$\bar{x}$|`=AVERAGE(A1:An)`|
|**2**|x~2~|n|`sample size`|
|**3**|x~3~|s^2|`=VAR(A1:An)`|
|**4**|..|Z|`Z-score for desired confidence`|
|**5**|..|Half Interval|`=C$3*SQRT(C$2/C$1)`|
|**6**|..|Lower Bound|`=B$1-B$5`|
|**7**|..|Lower Bound|`=B$1+B$5`|
|**n**|x~n~|||

If the sample size is small (as in the shopping cart example in chapter 2) then a slightly different formula applies using the [**t-distribution**](https://en.wikipedia.org/wiki/Student%27s_t-distribution)(<sup>3</sup>). 

Supposing as is so often the case with metrics generated by a web analytics tool we have only the average and the sample size, but no way to calculate the variance at all because we do not have the individual datapoints? In this case it is difficult to calculate any level of confidence, since we have literally no idea whether the mean is reasonably representative or wildly skewed by random outliers. This is another reason that canned metrics like 'average time on site' are of limited usefulnes. 

## References

1. Gumm, Bryan. 2013. “Metrics and the Statistics Behind A/B Testing.” In _A/B Testing: The Most Powerful Way to Turn Clicks into Customers_.

2. Beaulieu-Prévost, Dominic. 2006. “Confidence Intervals: From Tests of Statistical Significance to Confidence Intervals, Range Hypotheses and Substantial Effects.” _Tutorials in Quantitative Methods for Psychology_ 2 (1):11–19.

3. Rumsey, Deborah J. 2011. _Statistics for Dummies, 2nd Edition_.

