---
title: Linear Regression
weight: 3
---

# Linear Regression

Now that we have introduced somewhat more formally [the learning problem]({{<ref "../../learning-problem">}}) and its notation lets us study a simple but instructive regression problem from Chapter 1 of Bishop's book that is known in the statistics literature as *shrinkage*. Note that in many figures below the label is denoted as $t$ rather than $y$ as used in the equations below.

Suppose that we are given the training set  $\mathbf{x} = \{x_1,...,x_m\}$ together with their labels, the vectors $\mathbf{y}$. We need to construct a model such that a *suitably chosen* loss function is minimized for a **different** set of input data, the so-called test set. The ability to correctly *predict* when observing the test set, is called **generalization**. 

![Training dataset and Target Unknown Function](images/Figure1.2.png)
*Training Dataset (m=10) for the Regression Model. The green curve is the uknown target function.*

Since the output $y$ is a continuous variable then the supervised learning problem is called a regression problem (otherwise its a classification problem). The dataset is generated (in data scienece these datasets are called *synthetic*) by the function $sin(2 \pi x) + ϵ$ where $x$ is a uniformly distributed random variable and $ϵ$ is $N(\mu=0.0, \sigma^2=0.3)$. This target function is **completely unknown** to us - we just mention it here for completeness.  

Let us now pick the hypothesis set that correspond to polynomials of the following form,

$$g(\mathbf{w},x_i) = w_0 + w_1 x_i + w_2 x_i^2 + ... + w_M x_i^M$$

Our job is to find $\mathbf{w}$ such that the polynomial above fits the data we are given - as we will see there are multiple hypothesis that can satisfy this requirement. To gauge our investigation, we need to define a metric, an error or loss function in fact, that is also a common metric in regression problems of this nature. This is the Mean Squared Error (MSE) function. 

$$L(\mathbf{w}) = \frac{1}{2m} \sum_{i=1}^m \{(g(\mathbf{w},x_i)-y_i)\}^2$$

NOTE: Please note that the factor 2.0 in the denominator is for mathematical convenience.  When we take the derivative as we need to do in the training optimization procedure this factor will cancel the factor 2.0 of the derivative. 
. 
![Loss Function](images/Figure1.3.png)
*The loss function chosen for this regression problem, corresponds to the sum of the squares of the displacements of each data point and our hypothesis. The sum of squares in the case of Gaussian errors gives raise to an (unbiased) Maximum Likelihood estimate of the model parameters. Contrast this to sum of absolute differences.*

Now our job has become to choose two things: the weight vector $\mathbf{w^*}$ *and* $M$ the order of the polynomial. **Both** define our hypothesis.  If you think about it, the order $M$ defines the model complexity in the sense that the larger $M$ becomes the more the number of weights we need to estimate and store. Obviously this is a trivial example and storage is not a concern here but treat this example as instructive for that it applies in many far for complicated settings. 



<img src="images/Figure1.4a.png" width="40%"> <img src="images/Figure1.4b.png" width="40%">
<img src="images/Figure1.4c.png" width="40%"> <img src="images/Figure1.4d.png" width="40%">


Obviously you can reduce the training error to almost zero by selecting a model that is complicated enough (M=9) to perfectly fit the training data (if m is small).  

![Loss Function](images/Figure1.5.png)

But this is not what you want to do. Because when met with test data, the model will perform far worse than a less complicated model that is closer to the true model (e.g. M=3). This is a central observation in statistical learning called **overfitting**. In addition, you may not have the time to iterate over M (very important in online learning settings). 

To avoid overfitting we have multiple strategies. One straightforward one is evident by observing the wild oscillations of the $\mathbf{w}$ elements as the model complexity increases. We can penalize such oscillations by introducing the $l_2$ norm of $\mathbf{w}$ in our loss function.

$$L(\mathbf{w}) = \frac{1}{2} \sum_{i=1}^m \{(g(\mathbf{w},x_i)-y_i)\}^2 + \frac{\lambda}{2} ||\mathbf{w}||^2$$

This type of solution is called **regularization** and because we effectively shrink the weight dynamic range it is also called in statistics shrinkage or ridge regression. We have introduced a new parameter $\lambda$ that regulates the relative importance of the penalty term as compared to the MSE. This parameter together with the polynomial order is what we call *hyperparameters* and we need to optimize them as both are needed for the determination of our final hypothesis $g$. 

The graph below show the results of each search iteration on the $\lambda$ hyperparameter.

![Loss Function](images/Figure1.8.png)


Lets reflect on the MSE and how model complexity gives raise to various generalization errors. 

$$MSE = \mathbb{E}[\hat{y}_i - y_i)^2] = \mathrm{Bias}(\hat{y}_i)^2 + \mathrm{Var}(\hat{y}_i)$$

which means that the [MSE captures both bias and variance](https://en.wikipedia.org/wiki/Mean_squared_error) of the estimated target variables and as shown in the plots above, increasing model capacity can really increase the variance of $\hat{y}$. We have seen that as the $\mathbf{w}$ is trying to exactly fit, or memorize, the data, it minimizes the bias (in fact for model complexity M=9 the bias is 0) but it also exhibits significant variability that is itself translated to $\hat{y}$. Although the definition of model *capacity* is far more rigorous, we will broadly associate complexity with capacity and borrow the figure below from Ian Goodfellow's book to demosntrate the tradeoff between bias and variance. What we have done with regularization is to find the $\lambda$ that minimized generalization error aka. find the optimal model capacity. 

![generalization-error-vs-capacity](images/generalization-capacity.png)
*As capacity increases (x-axis), bias (dotted) tends to decrease and variance(dashed) tends to increase, yielding another U-shaped curve for generalization error (bold curve). If we vary capacity along one axis, there is an optimal capacity, with underﬁtting when the capacity is below this optimum and overﬁtting when it is above.*

## Bias and Variance Decomposition during the training process

Apart from the composition of the generalization error for various model capacities,  it is interesting to make some general comments regarding the decomposition of the generalization error (also known as empirical risk) during training. Early in training the bias is large because the network output is far from the design function. The variance is very small because the data has had little influence yet. Late in training the bias is small because the network has learned the underlying function. However if train for too long then the network will also have learned the noise specific to the dataset (overfitting). In such case the variance will be large because the noise varies between training and test datasets. 


## Implementing linear regression

This is a notebook that demonstrates the exact same example above.

<iframe src="https://nbviewer.jupyter.org/github/pantelis-classes/PRML/blob/master/notebooks/ch01_Introduction.ipynb" width="900" height="1200"></iframe>
