---
title: Identifying Bias and Correcting for Fairness
---

#  Identifying Bias and Correcting for Fairness

![ibm-fairness-pipeline](images/ibm-fair-pipeline.png)
*IBM's Fairness Pipeline*

When you are asked to perform a data mining task (e.g. classification, regression) you are more often than not given "dirty" data that you need to glean to address a number of issues such as data errors, missing data etc. These gleaning tasks are the easy part and standard APIs do exist to enable you to analyze data for each of these issues and perform the necessary corrective actions. 

The most difficult and dangerous challenge you are facing though as data scientists are _hidden_ issues - the most prevalent of them is _bias_. Your task is to learn and demonstrate the usage of fair ML systems that detect and remove bias from datasets. 

In this project you are given a dataset that is associated with [financial credit](https://archive.ics.uci.edu/ml/datasets/Statlog+%28German+Credit+Data%29) and you are asked to use the [IBM's AI Fairness 360 toolkit](http://aif360.mybluemix.net/) in your Colab notebook environment to complete the following steps:

1. Read the [paper](https://arxiv.org/abs/1810.01943) and _fully_ understand the fairness pipeline. Write your own tutorial summary of the pipeline in a markdown file. (25 points)
2. Execute the [credit decision pipeline](https://nbviewer.jupyter.org/github/IBM/AIF360/blob/master/examples/tutorial_credit_scoring.ipynb) that is detecting age bias and removing using the reweighting algorithm and explain the findings.  (25 points)
3. Apply a different method for detecting and removing bias. (25 points)
4. Write a thorough explanation comparing the reweighting and the method you selected. (25 points) 

Feel free to incorporate in one notebook everything or to type the documentation parts in a separate markdown file.  
