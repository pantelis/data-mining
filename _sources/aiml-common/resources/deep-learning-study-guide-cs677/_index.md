---
title: Study Guide for CS677 
---

# Study Guide for CS677

**General guidelines**

1. Study from the notes and focus on critically understanding the concepts. Read from the two books _only_ the _whole_ sections that overlap with the notes using the syllabus as the guide.   
2. There will be no definition questions e.g. what is a decision tree. 
3. There will be no  mathematical derivations (all formulas needed will be given). 
4. Some questions will be computational - make sure you have access to a calculator 
5. Some questions will be multiple choice
6. Some questions will include a figure and you will be asked to explain it. 

**Logistics**

1. Conference in at the time of the exam and turn on your camera. Make sure you are in a place that is quiet and no one will interrupt you.
2. Link to the test will be given to you on Webex, you need to download it and bring it up on the screen. 
3. You need to have empty sheets of paper, pencil / pen and eraser. 
4. Ask clarification questions via conference chat sent to "Everyone" so other can benefit from the responses.  
5. Smartphones will be allowed only at the end to scan your write ups and upload them into canvas. To scan you need to use CamScanner or GeniousScan or any other app of your choice that can generate PDF files of your scans. in your smartphones. 
6. At the end of the exam you will upload into the corresponding Canvas assignment your pdf file(s) **AND** send then by email to the TA. You need to use your University email account for that. 

**Topics**

| Topic    |  What to pay attention to   |
| --- | --- |
|  The learning problem   |  1. Understand the block diagram of supervised problem with the math.  |
| ML Estimation | 1. Understand what ML estimation is doing and be prepared to answer questions as to how it differs from the Bayesian setting. | 
|  Linear Regression  | 1. Understand what is regularization and how over-fitting is manifested.   |
|  Classification  |  1. Understand the problem setting and especially the classification metrics.   |
|  Back-propagation | 1. You may be given a simple network and ask to back-propagate it. | 
|  Optimization  |  1. Pay close attention how the gradient descent works and its behavior as it searches the space of weights. |   
| CNNs | 1. Understand the architecture elements and how they help in the learning process.  2. Understand how ResNets differ with earlier architectures such as VGG16 | 


## Q&A on Optimization / Training

1. Suppose the features in your training set have very different scales. We have seen that normalization of the input helps but why normalization is even more important when we use L2 regularization? 

Since regularization penalizes large weights, features with smaller values will tend to be ignored compared to features with larger values.

2. Can Gradient Descent get stuck in a local minimum when training a Logistic Regression model?

Gradient Descent cannot get stuck in a local minimum when training a Logistic Regression model because the cost function is convex.

3. Do all Gradient Descent algorithms lead to the same model, provided you let them run long enough?

If the optimization problem is convex (such as Linear Regression or Logistic Regression), and assuming the learning rate is not too high, then all Gradient Descent algorithms will approach the global optimum and end up producing fairly similar models. However, unless you gradually reduce the learning rate, Stochastic GD and Mini-batch GD will never truly converge; instead, they will keep jumping back and forth around the global optimum. This means that even if you let them run for a very long time, these Gradient Descent algorithms will produce slightly different models.

4. Suppose you use Batch Gradient Descent and you plot the validation error at every epoch. If you notice that the validation error consistently goes up, what is likely going on? How can you fix this?

If the validation error consistently goes up after every epoch, then one possibility is that the learning rate is too high and the algorithm is diverging. If the training error also goes up, then this is clearly the problem and you should reduce the learning rate. However, if the training error is not going up, then your model is overfitting the training set and you should stop training.

5. Is it a good idea to stop Mini-batch Gradient Descent immediately when the validation error goes up?

Due to their random nature, neither Stochastic Gradient Descent nor Mini-batch Gradient Descent is guaranteed to make progress at every single training iteration. So if you immediately stop training when the validation error goes up, you may stop much too early, before the optimum is reached. A better option is to save the model at regular intervals; then, when it has not improved for a long time (meaning it will probably never beat the record), you can revert to the best saved model.

6. Which Gradient Descent algorithm (among those we discussed) will reach the vicinity of the optimal solution the fastest? Which will actually converge? How can you make the others converge as well?

Stochastic Gradient Descent has the fastest training iteration since it considers only one training instance at a time, so it is generally the first to reach the vicinity of the global optimum (or Mini-batch GD with a very small mini-batch size). However, only Batch Gradient Descent will actually converge, given enough training time. As mentioned, Stochastic GD and Mini-batch GD will bounce around the optimum, unless you gradually reduce the learning rate.

7. Suppose you are using Ridge Regression and you notice that the training error and the validation error are almost equal and fairly high. Would you say that the model suffers from high bias or high variance? Should you increase the regularization hyperparameter α or reduce it?

If both the training error and the validation error are almost equal and fairly high, the model is likely underfitting the training set, which means it has a high bias. You should try reducing the regularization hyperparameter $\lambda$.
