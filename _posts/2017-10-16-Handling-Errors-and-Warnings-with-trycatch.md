---
layout: single
title: "Handling Error and Warnings with tryCatch()"
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - R
tags:
  - R
  - tryCatch
  - error handling
  - warning handling
excerpt: "I am currently working on implementing pangenome-wide association study (PGWAS) calculations in R using Fisher's exact test. The final program should essentially be able to calculate the strength of associations between traits (e.g. presence/absence of disease) and the genes in a set. One line in my original code encountered a problem:"
---

I am currently working on implementing pangenome-wide association study (PGWAS) calculations in R using Fisher's exact test. The final program should essentially be able to calculate the strength of associations between traits (e.g. presence/absence of disease) and the genes in a set. One line in my original code encountered a problem:

```
pval <- fisher.test(count,alternative="two.sided")$p.value
```

<!-- readmore -->
