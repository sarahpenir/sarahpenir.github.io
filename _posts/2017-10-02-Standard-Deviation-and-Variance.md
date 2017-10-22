---
layout: single
title: "Standard Deviation and Variance"
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Statistics
tags:
  - Bessel's correction
  - standard deviation
  - statistics
  - variance
mathjax: true

---

One of the tools that we discussed in our Data Analytics class last week was canonical correlation analysis (CCA). I won’t delve into CCA as I haven’t fully understood it yet, but my limited apprehension of this paper by <a href="http://www.tandfonline.com/doi/abs/10.1207/s15327752jpa8401_09">Sherry and Henson (2005)</a> tells me that it examines the relationship between two variable sets (usually in the form of predictor and response variables) using their shared variance. When I tried to define variance on my own without referring to a search engine, the only definition I came up with is that variance is the square of standard deviation (SD). Evidently, my understanding of the concept is insufficient, prompting me to brush up on the topic some people would categorize as basic.

<!-- readmore -->

Both variance and SD are measures of dispersion of the data relative to the mean (i.e. how spread out the numbers are from the mean). Let’s start with <b>variance</b>. It has two different formulas, one for a population and one for a sample. Imagine the population as the universal set and the sample as the subset of the population. <b>Population variance</b> is the average of the squared distances of each element from the mean:

$$
\begin{equation}
\sigma^{2}=\frac{\sum(X_{i}-\overline{X})^{2}}{N},
\end{equation}
$$

where $$\sigma^{2}$$ = variance, $$X_{i}$$ = value of the ith element, $$\overline{X}$$ = mean of the population, $$N$$ = number of elements.

<b>Sample variance</b>, on the other hand, exhibits a slight difference from the population variance in terms of its denominator (the $$N$$ becomes $$n-1$$):

$$
\begin{equation}
s^{2}=\frac{\sum(x_{i}-\overline{x})^{2}}{n-1},
\end{equation}
$$

where $$s^{2}$$ = sample variance, $$x_{i}$$ = value of the ith element of the sample, $$\overline{x}$$ = mean of the sample, $$n$$ = sample size.

The use of $$(n-1)$$ instead of $$N$$ is called <a href="https://en.wikipedia.org/wiki/Bessel%27s_correction">Bessel’s correction</a>. The application of the formula of population variance to calculate the sample variance often leads to the underestimation of the <b>(unknown) actual population variance</b>— which means that deviations of the sample values from the mean of the sample are, on average, a little less than the deviations of those sample values from the (unknown) true population mean. Using an $$(n-1)$$ divisor apparently corrects for that underestimation. The Wiki article on Bessel’s correction contains the mathematical proof for this bias correction.

<b>Population SD and sample SD</b> are essentially the <b>square root of the population variance and the sample variance</b>, respectively. I’ve always been passive in imbibing statistical concepts taught in school, so in the spirit of curiosity, I actually questioned the difference between the applications of variance and SD. Fortunately, <a href="https://stats.stackexchange.com/questions/35123/whats-the-difference-between-variance-and-standard-deviation">one thread in StackExchange</a> had a simple explanation:

>They each have different purposes. The SD is usually more useful to describe the variability of the data while the variance is usually much more useful mathematically. For example, the sum of uncorrelated distributions (random variables) also has a variance that is the sum of the variances of those distributions. This wouldn’t be true of the SD. On the other hand, the SD has the convenience of being expressed in units of the original variable.

I am ashamed to admit that this is probably the first time I genuinely grasped the substance of variance and SD. I’ve yet to check whether it’ll improve my comprehension of canonical correlation analysis.
