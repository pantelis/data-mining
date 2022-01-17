---
title: Model Fairness
draft: true
---

# Model Fainess

In the summer of 2020, huge protest in the US and around the world, prompted by discriminatory - even criminal - behavior of, hopefully, few law enforcement officers, renew the urgency to be watchful data scientists, developing models that are fair. Fairness is intuitively understood by many to be synonymous to unbiased decision involving multiple groups or categories. In many instances such discriminatory ML models decide on people's lives or wellbeing, eroding society's trust in AI. Its a classic example but for those that are just diving into the topic, few years ago a jaw dropping Propublica article  https://www.propublica.org/article/machine-bias-risk-assessments-in-criminal-sentencing publicized the problem. Many big tech companies have released open source tools and libraries that we can use to double check our models - techniques are not perfect but increasingly becoming very good. 

The problem of fairness has many facets. We start with the problem of deriving representations that are fair. 

## Adversarial Learning Fair Representations

Following [this](https://arxiv.org/pdf/1801.07593.pdf) and [this](https://arxiv.org/pdf/1707.00075.pdf) treatments, in the easiest setting we are given the following task: Predict a categorical or real $y$ for a given input $x$. We assume we have a model

$$ y = f(r(x))$$

where $r(x)$ is a function that creates embeddings. Both $f$ and $r$ are arbitrary neural networks with parameters learned using usual stochastic gradient decent algorithms.  For each example, there exists a feature $z$ that we consider to be sensitive or protected, and for which we want our predictions to be independent of this feature. Note that $z$ is usually observed but _even if $z$ is not used as an input to $r$, it may be correlated with other observed features_. This is important and to understand it better lets use an example: Imagine you are developing the next generation job matching application that has AI components. For each resume you create via state of the art NLP representations that can be used to classify the applicant to be desirable or not for this job. Even if the race of the applicant is not observable or to state the obvious not considered by the classifier, other attributes of the resume (e.g. the name) can be highly correlated and act as proxies of the applicant's race. 

### Debiasing Metrics

| Fairness Metric                                      | Description                                                                     |
| ---------------------------------------------------- | ------------------------------------------------------------------------------- |
| Demographic Parity                                   | This means that the predicted label $\hat y$ is independent of the feature $z$. |
|                                                      | Mathematically this metric is:$p(\hat y) = p(\hat y \| z)$                      |
| Equality of Odds  also known as positive rate parity | Conditioned on $y$, $\hat y$ and $z$ are independent.                           |
| Equality of Opportunity                              |                                                                                 |