---
layout: single
title: "On Hadley Wickham, the Prolific R Developer"
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - R
tags:
  - R
  - ggplot2
  - dplyr
  - Hadley Wickham
---

I spent the entire November writing scripts to generate the figures for my thesis and finding ways to make my data appear lovely. While it sounds leisurely when phrased in that manner, it was actually a month full of scouring Stack Overflow and Github pages for answers, trial and error with infrequent successes, misdirected anger springing from frustration, and countless coffee breaks. The packages ```dplyr```, ```ggplot2```, ```reshape2```, and ```ggtree``` became my weapons of choice. I am actually fortunate to have had the opportunity to work with these packages several months earlier in prior engagements. Somehow it seems like the world knew what side quests and minor bosses to give me to prepare me for the final boss fight.

I hadn't given much thought about the big names in R until our Data Analytics professor mentioned this apparently prolific R developer named Hadley Wickham. A quick Google search of his name left me agape. He is guy who wrote all those R workhorse packages I am using! According to his <a href="hadley.nz">personal website</a>, his work can be divided into three categories: tools for data science (e.g. ```ggplot2```, ```dplyr```, ```stringr```), tools for data import (e.g. ```readr```, ```readxl```, ```rvest```), and software engineering (```devtools```, ```testthat```).  And so began my fascination with Wickham...

He completed his undergraduate studies at the University of Auckland (the same university where R was born), and earned his Ph.D. at Iowa State University for his dissertation entitled "Practical Tools for Exploring Data and Models" (the beginnings of ```ggplot``` and ```reshape```). For Wickham, tidy datasets have a specific structure: each variable is a column, each observation is a row, and each type of observational unit is a table-- a framework he distilled into ```tidyverse```, a coherent system of packages for data manipulation, exploration, and visualization.

I was particularly intrigued of Wickham because he represented this small subset of people dedicated to tool-building. Although tools are not ends in themselves, they help create the right environment for downstream analyses from which big conclusions could be made. In my mental hall-of-fame, Wickham has achieved the status of Heng Li, the primary author of the next-generation sequencing utilities ```SAMtools``` and ```Burrows-Wheeler aligner (BWA)```. 

Although it's easy to dismiss people like Wickham as prodigies, there's still much to learn from their habits that perhaps further elevate their natural talent. In a <a href="https://www.quora.com/What-does-a-typical-work-day-look-like-for-you">Quora thread</a>, he described his typical work day as follows:

>Generally, my goal is to avoid interruptions so that I can do “deep work” focussing intently on a single problem at a time. I turn off pretty much every notification that I can: I only allow a few apps on my phone to send notifications, I’ve turned off every slack notification that I can find, I only track active projects on github, and generally try to train myself to avoid caring about numbers (i.e. I have email folders that have >50,000 unread emails).

>Each week I try to pick just one or two bigger projects to work on (for example, I’m currently working on roxygen2 and staticdocs). It’s useful to have two things on the go so that if I get stuck on one I can work on something else while my brain works on problem in the background.
