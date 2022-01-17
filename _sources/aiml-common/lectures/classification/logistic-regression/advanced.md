---
title: Advanced Logistic Regression
---

<!-- The model has significant advantages in that it does require the estimation of far fewer parameters compared to the case where the class conditional distributions involved in the posterior were parametric. For example if we had Gaussian class conditionals we would had to estimate (using Maximum Likelihood) their parameters $\mathbf \mu$ and $\mathbf \Sigma$ that grow quadratically to the number of features $n$. With logistic regression we only have an evident linear relationship between parameters and features.   -->

The figure below shows the corresponding posterior distribution $p(\mathcal{C}_1|\mathbf{x})$

![posterior-two-class-example](images/Figure4.10a.png)
*The class-conditional densities for two classes, denoted red and blue. Here the class-conditional densities $p(\mathbf{x}|\mathcal{C}_1)$ and $p(\mathbf{x}|\mathcal{C}_2)$ are Gaussian*

![posterior-two-class-example](images/Figure4.10b.png)
*The corresponding posterior probability for the red class, which is given by a logistic sigmoid of a linear function of $\mathbf{x}$.*

<!-- As we said, with logistic regression **we skip the assumption about the class-conditional densities** as they add parameters to our problem that grow  quadratic to the number of dimensions and we attempt to find the $n$ parameters of the model directly (the number of features) and sure enough we will use ML to do so.  -->
