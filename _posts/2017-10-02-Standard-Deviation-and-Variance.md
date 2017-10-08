---
defaults:
  # _posts
  - scope:
      path: ""
      type: posts
    values:
      layout: single
      author_profile: true
      read_time: true
      comments: true
      share: true
      related: true
---

One of the tools that we discussed in our Data Analytics class last week was canonical correlation analysis (CCA). I won’t delve into CCA as I haven’t fully understood it yet, but my limited apprehension of this paper by Sherry and Henson (2005) tells me that it examines the relationship between two variable sets (usually in the form of predictor and response variables) using their shared variance. When I tried to define variance on my own without referring to a search engine, the only definition I came up with is that variance is the square of standard deviation (SD).  Evidently, my understanding of the concept is insufficient, prompting me to brush up on the topic some people would categorize as basic.

Both variance and SD are measures of dispersion of the data relative to the mean (i.e. how spread out the numbers are from the mean). Let’s start with variance. It has two different formulas, one for a population and one for a sample. Imagine the population as the universal set and the sample as the subset of the population. Population variance is the average of the squared distances of each element from the mean:
