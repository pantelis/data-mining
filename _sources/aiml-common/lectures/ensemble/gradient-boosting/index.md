# Gradient Boosting

Like AdaBoost, Gradient Boosting works by sequentially adding predictors to an ensemble, each one correcting its predecessor. However, instead of tweaking the example weights at every iteration, this method tries to _fit the new predictor to the residual errors_ made by the previous predictor. 

The complete understanding of gradient boosting (and boosting in general) requires mathematical treatment around function-space optimization  as in [Friedma's original paper](https://statweb.stanford.edu/~jhf/ftp/trebst.pdf). Here we look at the solution from a practical perspective and attempt to understand it with the use of a regression example as shown below. 

## Gradient Boosting for Regression Example

![gradient-boost-example](images/gradient-boost-example.png)
*In this depiction of Gradient Boosting, the first predictor (top left) is trained normally, then each consecutive predictor (middle left and lower left) is trained on the previous predictor’s residuals; the right column shows the resulting ensemble’s predictions which is equal to the sum of the predictions of the trees involved.*

Predictions improve as the number of trees grows but we need to know when to stop. 

![gradient-boosting-performance](images/gradient-boosting-performance.png)
*On the left we  dont have enough trees to fit the training set, while the one on the right we have too many trees and overfit the training set.*


## XGBoost

In practice, do not use sklearn for gradient boosting. It is not an exaggeration to note that the optimized library for gradient boosting, **XGBoost** is a defacto tool for winning Kaggle competitions. Given that gradient boosting dominates performance wise many methods in classical machine learning with structured data (e.g. tabular data), XGBoost is also the standard library to try first in these type of problems. It offers also automatic ways of stopping at the right number of trees in the ensemble. [This write up](https://blog.mattbowers.dev/how-to-understand-xgboost) explains its internal design.
