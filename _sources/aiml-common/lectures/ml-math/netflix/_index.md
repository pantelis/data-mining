---
title: The Netflix Prize and Singular Value Decomposition
---

## Introduction
The following are based on the [winning submission paper](https://www.netflixprize.com/assets/GrandPrize2009_BPC_BellKor.pdf) as well as [their subsequent publication](https://datajobs.com/data-science-repo/Recommender-Systems-[Netflix].pdf). 

The Netflix Prize was an open competition for the best **collaborative filtering algorithm** to predict user ratings for films, based on previous ratings without any other information about the users or films, i.e. without the users or the films being identified except by numbers assigned for the contest.

The competition was held by Netflix, an online DVD-rental and video streaming service, and was open to anyone who is neither connected with Netflix (current and former employees, agents, close relatives of Netflix employees, etc.) nor a resident of certain blocked countries (such as Cuba or North Korea).[1] On September 21, 2009, the grand prize of US \$ 1,000,000 was given to the BellKor's Pragmatic Chaos team which bested Netflix's own algorithm for predicting ratings by 10.06\%

This competition is instructive since:

1. Collaborative filtering models try to capture the interactions between users and items that produce the different rating
values. However, many of the observed rating values are due to effects associated with either users or items, independently
of their interaction. A prime example is that typical CF data exhibit large user and item biases – i.e., systematic tendencies
for some users to give higher ratings than others, and for some items to receive higher ratings than others.
2. Observing the posted improvements in RMSE over time, the competition has become of little business value to Netflix after a while. This means that it was unlikely that any minute improvement to RMSE (e.g. 0.1%) will translate to additional revenue.
3. The 10% improvement goal was a lucky number after all. Netflix had no clue as to if this was the *right* number when they defined the terms. Any small deviation from this number, would have made the competition either too easy or impossibly difficult.

## Problem statement
You are given the following dataset structure (will be explained in class) shown below,

![netflix-dataset](images/netflix-dataset.png)



Assuming that the rating matrix A is an m x n matrix with m users (500K) and n items (17K movies), this matrix is extremely sparse - it has only 100 million ratings, the remaining 8.4 billion ratings are missing (about 99% of the possible ratings are missing, because a user typically rates only a small portion of the movies). 

Given the very large data matrix it was only expected that competitors attempted to work out some form of dimensionality reductions and as it turns out this was the basis for the winning algorithm. If you recall the premise of SVD from linear algebra, it is a decomposition that can work with rectangular matrices and can result into a decomposition of the following kind:

$$A = U \Sigma V^†$$

where  $\mathbf{U}$ is a $m \times m$ real unitary matrix, $\mathbf{\Sigma}$ is an $m \times n$ rectangular diagonal matrix with non-negative real numbers on the diagonal, and $\mathbf{V}$  is a $n \times n$ real unitary matrix. Remember that a unitary matrix $U$ is a matrix that its conjugate transpose $U^†$ is also its inverse - its the complex analog of the orthogonal matrix and we have by definition $UU^†=I$.  

The columns of $U$ are eigenvectors of $AA^T$, and the columns of $V$ are eigenvectors of $A^TA$. The $r$ singular values on the diagonal of $\Sigma$ are the square roots of the nonzero eigenvalues of both $AA^T$ and $A^TA$.

It is interesting to attribute the columns of these matrices with the four fundamental subspaces:

1. The column space of $A$ is spanned by the first $r$ columns of $U$.
2. The left nullspace of $A$ are the last $m-r$ columns of $U$.
3. The row space of $A$ are the first $r$ columns of $V$.
4. The nullspace of $A$ are the last $n-r$ columns of V. 

We can write the SVD as,

$$A = U \sqrt{\Sigma} \sqrt{\Sigma} V^†$$

and given the span of the subspaces above we can now intuitively think what the terms $\mathbf{p}_u = U \sqrt{\Sigma}$ and $\mathbf{q}_i = \sqrt{\Sigma} V^†$ represent. 

![svd-netflix](images/svd-netflix.png)
*SVD decomposition reveals latent features weighted by the underlying singular values of the data matrix*

The first term represents the column space aka. it provides a representation of all inter-user factors (also called latent features, latent means hidden).  The second term represents the row space aka. it provides a representation of all inter-movie factors. Which brings us to the major point of what the $\sqrt{\Sigma}$ is doing to both terms. It represents the significance of those factors and therefore we can very easily use the singular values it contains to "compress" our representation by selecting the $k$ largest singular values and ignoring the rest.

Given these vectors of factors we can now use them to predict the rating:

![svd-netflix-prediction](images/svd-netflix-prediction.png)
*Prediction of a rating is the product between user latent features and movie latent features matrices.

For an intuitive description of the SVD solution see [here](https://sifter.org/~simon/journal/20061211.html).

<!-- ## Solution
We use the indexing notation to distinguish two different users $u,v$, and movies $i, j$. A rating $r_{ui}$ indicates
the preference by user $u$ of movie $i$. Values are ranging from 1 (star) indicating no interest to 5 (stars) indicating a strong
interest. We distinguish predicted ratings from known ones, by using the notation $\hat{r}_{ui}$ for the predicted value.
The scalar $t_{ui}$ denotes the time of rating $r_{ui}$. Here, time is measured in days, so $t_{ui}$ counts the number of days elapsed
since some early time point.  The $(u,i)$ pairs for which $r_{ui}$ is known are stored in the training set $K = \{ (u,i) | r_{ui} \}$. Notice that $K$ includes also the Probe set. Each user $u$ is associated with a set of items denoted by $R(u)$, which contains all the items for which ratings by $u$ are available. Likewise, $R(i)$ denotes the set of users who rated item $i$. Sometimes, we also use a set denoted by $N(u)$, which contains all items for which $u$ provided a rating, even if the rating value is unknown. Thus, $N(u)$ extends $R(u)$ by also considering the ratings in the Qualifying set. -->
