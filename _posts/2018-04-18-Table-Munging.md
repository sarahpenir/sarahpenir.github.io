---
layout: single
title: "R: Some Table Munging Tricks"
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - R
tags:
  - dplyr
  - reshape2
  - data.table
  - data frame
  - select data frame columns by vector of names using dplyr
  - sort data frame columns according to vector of names
  - sort data frame rows according to vector of names
  - cast multiple value.var columns using reshape2 and data.table
  
  

---

I've been working with huge tables lately (at least 50,000 rows or columns). Sometimes you think you know all the basic commands you need to string together to get through any trouble, until a seemingly easy problem comes along to break this notion into a million pieces. Here are some handy table munging tricks:

* [Select data frame columns by vector of names using dplyr](#select-data-frame-columns-by-vector-of-names-using-dplyr)  
* [Sort data frame columns according to vector of names](#sort-data-frame-columns-according-to-vector-of-names)
* [Sort data frame rows according to vector of names](#sort-data-frame-rows-according-to-vector-of-names)
* [Cast multiple value.var columns using ```reshape2``` and ```data.table```](#cast-multiple-valuevar-columns-using-reshape2-and-datatable)

<!-- readmore -->

### Select data frame columns by vector of names using dplyr

```R
> library(dplyr)
> df <- data.frame(col1=c(1,2,3), col2=c(4,5,6), col3=c(7,8,9), col4=c(10,11,12))
> df

  col1 col2 col3 col4
1    1    4    7   10
2    2    5    8   11
3    3    6    9   12

> vector <- c("col1","col3")
> df2 <- select_(df, .dots = vector)
> df2

  col1 col3
1    1    7
2    2    8
3    3    9
```

### Sort data frame columns according to vector of names

```R
> df <- data.frame(col1=c(1,2,3), col2=c(4,5,6), col3=c(7,8,9), col4=c(10,11,12))
> df
  
  col1 col2 col3 col4
1    1    4    7   10
2    2    5    8   11
3    3    6    9   12

> vector <- c("col3", "col2", "col1", "col4")
> df2 <- df[vector]
> df2

  col3 col2 col1 col4
1    7    4    1   10
2    8    5    2   11
3    9    6    3   12
```

### Sort data frame rows according to vector of names

```R
> df <- data.frame(name=letters[1:4], value=c(rep(TRUE, 2), rep(FALSE, 2)))
> df

  name value
1    a  TRUE
2    b  TRUE
3    c FALSE
4    d FALSE

> vector <- c("c", "b", "a", "d")
> df2 <- df[match(vector, df$name),]
> df2

  name value
3    c FALSE
2    b  TRUE
1    a  TRUE
4    d FALSE
```

Note: Both ```df``` and ```vector``` must have identical elements and not contain duplicate values.

### Cast multiple value.var columns using reshape2 and data.table

``` R
> library(reshape2)
> library(data.table)
> df <- data.frame(x1 = rep(1:3, each = 3),
+                  x2 = letters[rep(1:3, 3)],
+                  col1 = sample(10, 9, TRUE),
+                  col2 = sample(7, 9, TRUE))
> df

  x1 x2 col1 col2
1  1  a    4    2
2  1  b    8    7
3  1  c   10    5
4  2  a    9    7
5  2  b    1    7
6  2  c    6    2
7  3  a    3    4
8  3  b    2    1
9  3  c    7    3

> df2 <- dcast(setDT(df), x1 ~ x2, value.var=c("col1", "col2"))
> df2

   x1 col1_a col1_b col1_c col2_a col2_b col2_c
1:  1      4      8     10      2      7      5
2:  2      9      1      6      7      7      2
3:  3      3      2      7      4      1      3 
```
