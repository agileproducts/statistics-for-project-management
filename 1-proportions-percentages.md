---
title: "Proportions and Percentages"
bibliography: "bibliography.yaml"
---

> A good metric is a ratio or a rate  - *Lean Analytics*, @item1

Probably the simplest and most common type of product measurement is to count two things and divide one by the other, for example the number of people who see a webpage and the number of people who click a button on that page. The result is a proportion, and is often expressed as a percentage. 

```{.math}
Number of page visitors = 1000
Number of button clicks = 100

Proportion of visitors clicking the button = 100/1000 = 0.1
As a percentage 0.1 x 100 = 10%
```

This is elementary arithmetic. The common mistake to avoid is quoting the result to too much precision, using lots of decimal places which aren't justified or aren't informative. 

## Decimal places and significant figures

Imagine sending out an email promotion each month to 10,000 people, and obtaining the following results:

||Month 1|Month 2|Month 3|
|-|-|-|-|
|Received|10000|10000|10000|
|Opened|1830|1778|1742|
|Clicked|723|690|652|
|Open rate|18.30%|17.78%|17.42%|
|Click rate|7.23%|6.90%|6.52%|

Quoting percentages to two decimal places as we have done here is very common practice. Some style guides suggest this (@item2), and it is the default setting for percentage formats in spreadsheets or in tools like Google Analytics. But consider how much precision is implied by knowing a ratio to the nearest 0.01%. That’s 0.0001, or one part in ten-thousand. 

In our email example we have exactly 10,000 recipients, so quoting those response rates to two decimal places means reporting to a precision of one individual person. Do we really care if one person more or less opens the mail? Can we reasonably say anything about the relative performance of each mailer to that level of granularity?

When quoting and rounding numbers we must consider whether digits are **significant** and whether they are **effective**. A fraction can only be quoted a maximum of the same number of [significant figures](https://en.wikipedia.org/wiki/Significant_figures) as exists in the [least precise](https://en.wikipedia.org/wiki/Significance_arithmetic#Multiplication_and_division_using_significance_arithmetic) of the numbers used to calculate it. On this basis with a denominator of 10000 we could just about get away with quoting 1778 out of 10000 as '17.78%', but we could certainly not quote 1778 out of 10001 as '17.778%'. However in this case that last decimal place does not convey any effective information, since it represents the action of only a handful of individuals. It would be better to round these numbers to one decimal place, reporting click-through rates of 7.2, 6.9 and 6.5%. 

Were we to scale everything back by a factor of ten and send out 1000 emails with open counts of '72', '69' and '65' then we should not quote the CTR to the same precision - we’d be back in a situation where the random action of just a handful of individuals impacted the result. Here we would have to say the rate was a uniform 7%. At the other end of the spectrum if we sent out an email to one million people then it would be silly to quote the CTR to the nearest 0.0001%, as again these digits while significant would not be effective. Here the style-guide standby of two decimal places would probably suffice. 

If the numbers are samples of a large population then the level of precision to which they can be quoted becomes a matter of statistics, for which see [chapter 3](../chapter-3/index.html). 

## Relative vs absolute difference

One of the reasons ratios are preferred as metrics is that they are inherently comparable - we can send out an email to twice as many people this month as we did last month, but still compare the open and click-through rates to see which performed better. One aspect of this that can trip people up is to explain *how* they are different from each other, and whether to express that difference in relative or absolute terms. 

Suppose we have a click-through rate of 4% one month and 6% the next. One way to describe this is to say that the rate went up by 2%. That's absolute terms. Alternatively we might say that the rate went up by 50% - since 6% is half as many again as 4%. That's relative terms. Mathematically:

```{.math}
Absolute difference = Percentage B - Percentage A

Relative difference = (Percentage B - Percentage A)/Percentage A
```

Which is correct? Both are equally valid, depending on context and the point you are trying to communicate. For a freemium product a rise in conversions to a paid tier from 1% to 1.5% might represent stellar success, provided it doesn't mean three individuals converting rather than two. For a mailer it is probably overdramatic to report a 25% collapse in clickthroughs when it has fallen from 4% one month to 3% the next, but it might not be if that represents a million people. Alarmist newspapers notoriously misuse this concept, producing screaming headlines that say the murder rate in a city has doubled, when it has risen from two murders in a year to four. Personally I find it easier to think in absolute numbers, but if in doubt the safest thing to do is report both the percentage ratio and the numbers that produced it. 

## Choosing a denominator

In product measurements coming up with the numerator - the number on top of the fraction - is usually pretty easy. You just count something. Choosing the right number to go on the bottom of the fraction - the denominator - can require more thought. Is it pageviews, visits, visitors, or unique visitors? All users, or just premium tier ones? Downloads, or installs? If it is difficult to figure out what the correct denominator is, or to measure it, then it may indicate a problem with the metric. 

## Fractions in plain language

We obtain numbers in order to understand something. Sometimes it is easier to arrive at and communicate that understanding if we set decimals and percentages aside and think in terms of simple words and fractions. It is perhaps easier to think about ‘one user in 300’ clicking a link than it is ‘0.35%’. Saying out loud that ‘0.56’ is 56 out of every 100 may better convey the precision implied in that number. Saying that ‘about a sixth’ of visitors come from Facebook may be more descriptive than quoting an average between 15 and 20%. This is how scientists and engineers often work, calculating things to precision but then sanity-checking the results with a bit of ready reckoning. 

## References