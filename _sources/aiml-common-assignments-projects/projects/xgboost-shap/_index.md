---
title: Interpretable Trees
---

# Interpretable Trees

{{%youtube -taOhqkiuIo%}}

Imagine we are tasked with predicting a person’s financial status for a bank. The more accurate our model, the more money the bank makes, but since this prediction is used for loan applications we are also legally required to provide an explanation for why a prediction was made. After experimenting with several model types, we find that gradient boosted trees as implemented in XGBoost give the best accuracy. Unfortunately, explaining why XGBoost made a prediction seems hard, so we are left with the choice of retreating to a linear model, or figuring out how to interpret our XGBoost model. No data scientist wants to give up on accuracy…so we decide to attempt the latter, and interpret the complex XGBoost model (which happens to have 1,247 depth 6 trees).

Read about one of the most popular blog posts [here](https://towardsdatascience.com/interpretable-machine-learning-with-xgboost-9ec80d148d27) to understand the problem and its solution provided by [Tree SHAP](https://proceedings.neurips.cc/paper/2017/hash/8a20a8621978632d76c43dfd28b67767-Abstract.html)

NOTE: SHAP is also [implemented in Google Cloud Platform](https://cloud.google.com/ai-platform/prediction/docs/ai-explanations/overview). 

Your tasks are as follows:

1. Checkout [this notebook](https://slundberg.github.io/shap/notebooks/Census%20income%20classification%20with%20XGBoost.html)
2. Make it work in Colab - produce in other words all the graphs that the author showcased. (15 points)
3. Understand  the Tree SHAP method and write a 4 page summary of your intuition of **how** it is offering interpretability in ensemble methods  (35 points)
4. Apply the Tree SHAP method to the [Kaggle house price prediction problem](https://www.kaggle.com/c/house-prices-advanced-regression-techniques) that uses XGBoost for the predictions. What is the minimal set of features you would use to predict house prices given the dataset? (50 points) 


Rubric:

1. N/A
2. Your notebook must run. All data needed must be downloaded and the execution must be flawless when someone executes all cells.
3. Your report must be single spaced and can be authored in standalone md (with png images) or embedded md in a notebook that will also display the images / plots your need to demonstrate your understanding of the Tree SHAP method. 
4.  You have to use XGBoost and Tree SHAP for this regression problem. Like in 3 above all cells must execute flawlessly. You clearly state the minimal list of features you would use for prediction and indicate the plots that demonstrate your opinion. 


