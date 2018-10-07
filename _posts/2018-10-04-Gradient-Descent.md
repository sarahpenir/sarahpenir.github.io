---
layout: single
title: "Linear Regression and Gradient Descent"
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - 
tags:
  - 
mathjax: true 

---

Sometime ago, when I thought I didn't have any on my plate (a gross miscalculation as it turns out) during my post-MSc graduation lull, I applied for a financial aid for Andrew Ng's Machine Learning course in Coursera. Having been a victim of the all too common case of very smart people being unable to explain themselves well and given Ng's caliber, I didn't think I would be able to wrap my head around the lectures. I'm on my 8th week now, and it's honestly one of the things I look forward to when weekends roll around. However, my brain's wiring dictates that my understanding of any concept only becomes granular when I force myself to write about it. Here is an attempt at linear regression and gradient descent.

<!-- readmore -->

## Simple Linear Regression
In a simple linear regression problem, the relationship between two variables $$x$$ and $$y$$ (or $$h{_{\theta}}(x)$$) is governed by the line equation:

$$
\begin{equation}
h{_{\theta}}(x) = \theta_{0} + \theta_{1}x,
\end{equation}
$$

where $$\theta_{1}$$ is the slope of the line, and $$\theta_{0}$$ is the y-intercept.

It is used to predict values with a constant slope and within a continuous range. The idea is to fit this hypothesis to a training (existing) data so that it may be used to estimate $$y$$ based on $$x$$. Essentially, we need to look for the appropriate values for parameters $$\theta_{0}$$ and $$\theta_{1}$$.

## Cost Functions
What metric do we use to determine whether a combination of parameters is a good fit? Cost functions serve as a measure of how well or wrong the model is performing in terms of estimating the relationship between $$x$$ and $$y. Cost functions are typically expressed as the difference between the predicted value and the actual value. In the case of linear regression, the mean squared error (MSE) function is used:

\begin{equation}
J(\theta _{_{0}}, \theta _{_{1}}) = \frac{1}{2m}\sum_{i=1}^{m}(h_{\theta }(x^{(i)}) - y^{(i)})^{2}
\end{equation}

Our ultimate goal is to minimize the cost function. In other words, we want to minimize the difference between the predicted and actual values (minimize $$J(\theta _{_{0}}, \theta _{_{1}})$$).

## Gradient Descent
Keeping in mind that our ultimate goal is to minimize the cost function $$J(\theta _{_{0}}, \theta _{_{1}})$$, we can start with some random values for $$\theta_{0}$$ and $$\theta_{1}$$, and keep changing or updating the values until we end up at a minimum. To implement this, we can use gradient descent, an efficient optimization algorithm that allows a model to learn the gradient or direction it should take to reduce errors. The algorithm can be formally presented as follows: 

\begin{equation}
\text{ repeat until convergence \{}\\
\theta_j{} := \theta_j{} - \alpha \frac{\partial }{\partial \theta_j{}}J(\theta_0, \theta_1)\\
\text{ (for j = 1 and j = 0)}\\
\}
\end{equation}

where alpha or the learning rate or how quickly we approach the minimum.

We know we have succeeded when the cost function is at its minimum. Graphically, if we put theta0 on the x-axis, theta1 on the y-axis, and the cost function on the vertical , z-axis, this looks like reaching the bottom area of this graph.

## Linear Regression with Multiple Variables
For multivariate linear regression, wherein multiple correlated dependent variables are being predicted, the gradient descent equation maintains the same form and is repeated for the “n” features being taken into consideration:
(insert formula)

## Learning Rate
Caution must be exercised when choosing the learning rate alpha. A sufficiently small alpha will cause the cost function J(theta) to decrease on very iteration. However, if alpha is too small, the gradient descent will take a while to converge. If alpha is too large, J(theta) may not decrease on every iteration and may fail to converge.

## Speeding Up Gradient Descent
The process of converging to a minimum can be sped through two techniques, namely feature scaling and mean normalization. Feature scaling refers to the process of framing the features within the -1 < x < 1 range, and it involves dividing the input values by the range of the input variable (i.e. maximum value minus the minimum value). Mean normalization, on the other hand, necessitates the subtraction of an average value from the values, in order to make the features have an approximately zero mean. To implement feature scaling and mean normalization, the input values can be adjusted as follows:
(insert formula)

## Implementation of Linear Regression in R


