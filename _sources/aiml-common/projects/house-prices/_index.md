---
title: House Prices 
---

# House Prices

![houses image](housesbanner.png)

## Description
Ask a home buyer to describe their dream house, and they probably won't begin with the height of the basement ceiling or the proximity to an east-west railroad. But [this competition's dataset](https://www.kaggle.com/c/house-prices-advanced-regression-techniques) proves that *much more* influences price negotiations than the number of bedrooms or a white-picket fence. Predict sales prices and practice feature engineering using regression methods of your choice.  

## Goal
It is your job to predict the sales price for each house. For each Id in the test set, you must predict the value of the SalePrice variable. 

## Metric
Submissions are evaluated on Root-Mean-Squared-Error (RMSE) between the logarithm of the predicted value and the logarithm of the observed sales price. (Taking logs means that errors in predicting expensive houses and cheap houses will affect the result equally.)

## Submission File Format
The file should contain a header and have the following format:

Id,SalePrice
1461,169000.1
1462,187724.1233
1463,175221
etc.

You can download an example submission file (sample_submission.csv) on the [Data](https://www.kaggle.com/c/house-prices-advanced-regression-techniques/data) page.

