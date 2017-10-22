---
layout: single
title: "Warning and Error Handling with tryCatch()"
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - R
tags:
  - trycatch
  - R
  - error handling
  - warning handling
header:
  teaser: "https://sarahtakesnotes.files.wordpress.com/2017/10/1200px-nullset-svg.png"
---

A few weeks ago, I worked on an implementation of Fisher's exact test in R. The script expects a data frame with rows representing the various cases/phenotype of my bacterium, and columns corresponding to the presence or absence of certain genes as detected by <a href="https://github.com/katholt/srst2">SRST2</a>. Fisher's exact test, which is said to work well with small sample sizes, examines the association between two categorical variables (e.g. whether the presence or absence of a gene is linked to the manifestation of a phenotype). Implementing it in R was a matter of calling the ```fisher.test()``` function on a 2x2 contingency table called ```count.df``` to generate the p-values:
<!-- readmore -->

```R
pval <- fisher.test(count.df,alternative="two.sided")$p.value
```
But alas, it wasn't that easy since some of my count tables certainly had only one row or column (i.e. lack of intersection between the variables); hence, this error message in the console:

```R
Error in fisher.test(count.df, alternative = "two.sided") : 'x' must have at least 2 rows and columns
```
I had to look for a way to ignore the errors and print ```NA``` instead. This is where the ```tryCatch()``` function comes in: it provides a mechanism for handling unusual conditions, including errors and warnings. ```tryCatch()``` follows the following syntax:

```R
output <- tryCatch({expr}, warning = function(w) {warning-handler-code}, error = function(e) {error-handler-code})
```
1. ```{expr}```: Expression to be evaluated
2. ```warning = function(w) {warning-handler-code}```: Handles the warnings, wherein ```{warning-handling-code}``` is the alternative value to be returned when ```{expr}``` generates a warning
3. ```error = function(e) {error-handler-code}```: Handles the errors, wherein ```{error-handler-code}``` is the alternative value to be returned when ```{expr}``` generates an error

For my implementation of Fisher's exact test to work, I wrapped my original expression with the ```tryCatch()``` function, so that every time an error is encountered, it returns ```NA```:

```R
pval <- tryCatch(fisher.test(count.df,alternative="two.sided")$p.value, error=function(e) NA)
```
