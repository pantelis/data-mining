# Logistic Regression 

You are interviewing with Google's data science team having the responsibility of predicting the Click Through Rate (CTR) of ads they place on multiple web properties. Your hiring manager keen on testing you out, suggests to download [this dataset](https://www.kaggle.com/competitions/avazu-ctr-prediction/data) and asks you to code up a model that predicts the CTR based on Logistic Regression. 

## Task 1: Environment Setup (10 points)

You will use the familiar docker container based dev environment and download the data from Kaggle and store them in a location accessible from your application code. You may [want to read for this task](https://www.kaggle.com/docs/api#interacting-with-datasets). 

## Task 2: Data Preprocessing (30 points)

Preprocess the data you are given to your liking. This may include dropping some columns you wont use, addressing noisy or missing data etc. 

Use Pandas 2.x as a  dataframe abstraction for this task. You can learn about Pandas here:

```{eval-rst}
.. youtube:: PcvsOaixUh8
```

Ensure that all tranformations are orchestrated using Dagster and ultimately you end up with a data asset you can use for the training and testing the classifier. You may iterate between training / testing and data preprocessing as needed.

## Task 3: Logistic Regression (40 points)

Implement the logistic regression solution to the prediction problem that can work with Stochastic Gradient Descent (SGD). 

Show clearly all equations of the gradient and include comments in either markdown or Python (inline to code) explaining every stage of processing. Also, highlight any enhancements you may have done to improve performance. You cant use SGDClassifier from scikit-learn for this task but you can use numpy, tensor manipulation libraries from PyTorch 2 or TF2.   

## Task 4: Performance Results (20 points)

Plot the final precision vs recall curve of your classifier. Clearly explain the tradeoff between the two quantities and the shape of the curve. 














