---
title: COVID-19 Antibody Test
---

# COVID-19 Antibody Test

![drive-through-covid-test](images/drive-through-covid-test.jpeg)

You are a member of a data science team of a screening (test) site and the governor tasked you to provide statistics to his office about the aggregate antibody test results of former COVID19 patients. 

To plan "back to work" actions at the state level, one of the  metrics you need to estimate is the probability of a patient having antibodies given a positive $s$ test result. This is the probability $p(antibody | s=+)$.  

1. The facility is in a town where 1% of subjects have antibodies (and therefore 99% do not).
2. The [test kits are from a vendor](https://www.evaluate.com/vantage/articles/analysis/spotlight/covid-19-antibody-tests-face-very-specific-problem) and have the following characteristics: 80% of antibody test kits detect antibodies when they are present (and therefore 20% miss it). 9.6% of test kits detect antibodies when they are not there (and therefore 90.4% correctly return a negative result). Some vendors quote [these](https://en.wikipedia.org/wiki/Sensitivity_and_specificity) metrics. 

This is a classic application of the Bayes theorem:

$$p(a|b) = p(b|a)p(a)/p(b)$$

In late May 2020 doctors tried to point its behavior e.g in [CNN](https://www.cnn.com/videos/health/2020/05/27/coronavirus-covid-19-antibody-testing-cdc-sanjay-gupta-cpt-vpx.cnn);

The prior probability $p(antibody)$ that the doctor in the clip above called prevalence. Plugging the numbers, you get: 

$$p(a | s=+) = \frac{p(s=+| a)p(a)}{p(s=+)} = \frac{p(s=+|a)p(a)}{p(s=+|a)p(a)+p(s=+|not-a)p(not-a} = 7.7\%$$

This is amazing - only 7.7% of the people that get tested positive for antibodies do have them.  The number of false positives is very high. Can you guess what is happens when the same test kit is applied to Brooklyn (the epicenter of the epicenter in NYC) where the prior is much higher? 
