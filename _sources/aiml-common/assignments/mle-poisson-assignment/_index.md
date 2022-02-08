---
title: MLE - Poisson Assignment
---

# MLE - Poisson Assignment

Say you started a YouTube channel about a year ago. You’ve done quite well so far and have collected some data. You want to know the probability of at least x visitors to your channel given some time period. The obvious choice in distributions is the [Poisson distribution](https://en.wikipedia.org/wiki/Poisson_distribution) which depends only on one parameter, λ, which is the average number of occurrences per interval. We want to estimate this parameter using Maximum Likelihood Estimation.

1. (50 points) Simulate 100 visits to your youtube channel, assuming that they will a Poisson distribution with a mean of 10 visits per minute. Plot the arrival time vs visitor index. 

NOTE: To do this task make sure you read carefully the section Definitions and Probability Mass Function in [Poisson distribution](https://en.wikipedia.org/wiki/Poisson_distribution) entry of wikipedia and [this blog post](https://towardsdatascience.com/the-poisson-process-everything-you-need-to-know-322aa0ab9e9a). 

2.  (50 points)  Assume that you are given the visitation data generated in Step 1, implement a Gradient Descent algorithm from scratch that will estimate the Poisson distribution according to the Maximum Likelihood criterion. Plot the estimated mean vs iterations to showcase convergence towards the true mean. 

NOTE: To do this step, read [this blog post](https://towardsdatascience.com/understanding-maximum-likelihood-estimation-fa495a03017a) and note the negative  log likelihood function.  


RUBRIC: 

1. If you provide just the plots/code, you will be granted 50% of the points. To win the remaining 50% you will need clear documentation (see below). 
2. We need to see a clear explanation of all the stages of developing (1) and (2) above which means that you need to explain the code in a way that the writeup is understood by fellow students. 
3. Type inline with your Colab notebook your tutorial explanations. Equations can be typed in markdown using Latex syntax notation.  If you prefer plain Python you can also include markdown as a separate file but you do need to ensure that all plots are inline to that markdown document and are parsed correctly by Github. 
4. Submit by sharing the Colab or Github with the TA. 