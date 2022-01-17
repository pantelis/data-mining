---
title: Bayesian Optimization
---

In Bayesian regression or classification, we start with a prior $p_{model}(w)$ over the parameters $w$ of the $p_{model}(y|x, w)$ and form the initial posterior $p_{model}(w|x,y)$ using the Bayes rule. As the data are sequentially observed, the posterior is iteratively updated using the previous posterior and the new likelihood function $p_{model}(y|x,w)$ after receiving new data points. 

We can then form the predictive distribution and make predictions given new values of x:

$$p_{model}(y|x) = \int p_{model}(y|x,w)~p_{model}(w|x,y) ~ dw$$

Bayesian regression / classification is more complex than a plain MLE regression / classification.   No matter which of the two methods we use, we will always have hyperparameters in the learning process and evaluating the average loss is too expensive to obtain as it can only be obtained after training/validation/test runs for _each_ permutation of hyperparameters. 

When we have such as setting, we can apply the Bayesian Optimization (BO) approach that builds a probabilistic model of the underlying _loss function_. We can make the following analogies:

1. Instead of the data, $x$ now symbolizes the  _hyperparameters_ we try at each iteration.

2. Instead of the label, $y$ now symbolizes the _loss_ we get at each iteration.

So we have a regression problem of $x$ vs $y$ like before but now the semantics are different. There is an underlying target $p_{data}(y|x)$ function that we never get to know and we will try to approximate it with a $p_{model}$. We can now apply the sequential Bayesian approach in this problem.  According to Bayes,

$$p_{model}(y|x) = \frac{p_{model}(x|y)p_{model}(y)}{p_{model}(x)}$$

The prior component $p_{model}(y)$ that can be chosen from a family of models known to define a probability distribution over functions (the space of loss functions in its range $\mathbb R$). Gaussian Process Regression (GPR) with a radial basis function (RBF) or Matern kernels are commonly used. In Bayesian optimization the $p_{model}(y)$ is called the _surrogate_ model.  

If y* is the best loss observed so far, then we can define an approximation of the loss function that we call acquisition function - an analytical heuristic that will allow us to use in the place of the expensive loss function. This is called the Expected Improvement (EI) and is given by 

$$EI(x) = \mathbb E [\max(y-y^*, 0)]$$

where $y$ is sampled from the posterior. 

Optimizing the IE function with respect to $x$ leads to new candidate values of $x$ that we can try and see if they result in a new $y^*$ in a training/validation/test exercise. 

### References  

[BOTorch Overview](https://botorch.org/docs/overview)
