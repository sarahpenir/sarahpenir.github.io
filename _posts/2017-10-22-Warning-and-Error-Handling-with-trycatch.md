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
---

A few weeks ago, I worked on an implementation of Fisher's exact test in R. The script expects a data frame with rows representing the various cases/phenotype of my bacterium, and columns corresponding to the presence or absence of certain genes as detected by <a href="https://github.com/katholt/srst2">SRST2</a>. Fisher's exact test, which is said to work well with small sample sizes, examines the association between two categorical variables (e.g. whether the presence or absence of a gene is linked to the manifestation of a phenotype). Implementing it in R was a matter of calling the ```fisher.test()``` function on a 2x2 contingency table called ```count``` to come up with with the p-values:

<!-- readmore -->
```R
pval <- fisher.test(count,alternative="two.sided")$p.value
```
The brown fox jumped over the lazy dog.
