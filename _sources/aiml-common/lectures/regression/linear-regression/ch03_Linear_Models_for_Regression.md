---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

+++ {"id": "view-in-github", "colab_type": "text"}

<a href="https://colab.research.google.com/github/pantelis/PRML/blob/master/notebooks/ch03_Linear_Models_for_Regression.ipynb" target="_parent"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>

+++ {"id": "BxUAaIRR0pdK"}

# 3. Linear Models for Regression

```{code-cell} ipython3
---
colab:
  base_uri: https://localhost:8080/
  height: 34
id: TMxmVuag7eyA
outputId: c41915fc-7af0-4e1d-db57-85b8bd236b5b
---
from google.colab import drive
drive.mount('/content/drive')
```

```{code-cell} ipython3
:id: F3rYRMAD6ynO

# You need to adjust the directory names below for your own account
# e.g. you may elect to create ms-notebooks dir or not

# Execute this cell once

# 1. Download the repo and set it as the current directory
%cd /content/drive/My Drive/Colab Notebooks/ml-notebooks
!git clone https://github.com/pantelis/PRML
%cd /content/drive/My Drive/Colab Notebooks/ml-notebooks/PRML

# 2. install the project/module
!python setup.py install

```

```{code-cell} ipython3
---
colab:
  base_uri: https://localhost:8080/
  height: 34
id: iv9ADzLqiNsU
outputId: 147195c7-f211-423c-fc5d-0c51f8ac0a79
---
# 3. Add the project directory to the path
%cd /content/drive/My Drive/Colab Notebooks/ml-notebooks/PRML
import os, sys
sys.path.append(os.getcwd())
```

```{code-cell} ipython3
:id: qwxjFZSR_vuX

# Import seaborn
import seaborn as sns

# Apply the default theme
sns.set_theme()
```

```{code-cell} ipython3
:id: mrfT6d-50pdM

import numpy as np
from scipy.stats import multivariate_normal
import matplotlib.pyplot as plt
%matplotlib inline

from prml.preprocess import GaussianFeature, PolynomialFeature, SigmoidalFeature
from prml.linear import (
    BayesianRegression,
    EmpiricalBayesRegression,
    LinearRegression,
    RidgeRegression
)

np.random.seed(1234)
```

```{code-cell} ipython3
:id: btxxnn1A0pdQ

def create_toy_data(func, sample_size, std, domain=[0, 1]):
    x = np.linspace(domain[0], domain[1], sample_size)
    np.random.shuffle(x)
    t = func(x) + np.random.normal(scale=std, size=x.shape)
    return x, t
```

+++ {"id": "CUXJceLr0pdT"}

## 3.1 Linear Basis Function Models

```{code-cell} ipython3
---
colab:
  base_uri: https://localhost:8080/
  height: 322
id: 2mC2AOiR0pdU
outputId: 1df895ca-005e-410e-84f2-918f8edaa87b
---
x = np.linspace(-1, 1, 100)
X_polynomial = PolynomialFeature(11).transform(x[:, None])
X_gaussian = GaussianFeature(np.linspace(-1, 1, 11), 0.1).transform(x)
X_sigmoidal = SigmoidalFeature(np.linspace(-1, 1, 11), 10).transform(x)

plt.figure(figsize=(20, 5))
for i, X in enumerate([X_polynomial, X_gaussian, X_sigmoidal]):
    plt.subplot(1, 3, i + 1)
    for j in range(12):
        plt.plot(x, X[:, j])
```

+++ {"id": "3qMCArAb0pdY"}

### 3.1.1 Maximum likelihood and least squares

```{code-cell} ipython3
---
colab:
  base_uri: https://localhost:8080/
  height: 988
id: -88vjNA50pdY
outputId: 197079cc-9d1f-4e68-e87a-1b8df07e8a74
---
def sinusoidal(x):
    return np.sin(2 * np.pi * x)

x_train, y_train = create_toy_data(sinusoidal, 10, 0.25)
x_test = np.linspace(0, 1, 100)
y_test = sinusoidal(x_test)

M = 8

# Pick one of the three features below
feature = PolynomialFeature(M)
#feature = GaussianFeature(np.linspace(0, 1, M), 0.1)
# feature = SigmoidalFeature(np.linspace(0, 1, M), 10)

X_train = feature.transform(x_train)
X_test = feature.transform(x_test)
model = LinearRegression()
model.fit(X_train, y_train)

plt.figure(figsize=[10,8])
plt.plot(model.w) 
plt.xlabel("index of $w$")
plt.ylabel("$w$")

y, y_std = model.predict(X_test, return_std=True)

plt.figure(figsize=[10,8])

plt.scatter(x_train, y_train, facecolor="none", edgecolor="b", s=50, label="training data")
plt.plot(x_test, y_test, label="$\sin(2\pi x)$")
plt.plot(x_test, y, label="mean")
plt.fill_between(
    x_test, y - y_std, y + y_std,
    color="orange", alpha=0.5, label="std.")
plt.legend()
plt.xlabel("$x$")
plt.ylabel("$y$")

plt.show()
```

+++ {"id": "gXAvLZ7u0pdb"}

### 3.1.4 Regularized least squares

```{code-cell} ipython3
---
colab:
  base_uri: https://localhost:8080/
  height: 485
id: ChBt_3n70pdb
outputId: d479becc-bef9-45b1-f2a9-67d4c9e2d2e0
---
model = RidgeRegression(alpha=1e-3)
model.fit(X_train, y_train)
y = model.predict(X_test)

plt.figure(figsize=[10,8])
plt.scatter(x_train, y_train, facecolor="none", edgecolor="b", s=50, label="training data")
plt.plot(x_test, y_test, label="$\sin(2\pi x)$")
plt.plot(x_test, y, label="prediction")
plt.legend()
plt.show()
```

+++ {"id": "EpQP0Opk0pde"}

## 3.2 The Bias-Variance Decomposition

```{code-cell} ipython3
---
colab:
  base_uri: https://localhost:8080/
  height: 944
id: TE8CAbuO0pdf
outputId: a75c1cc4-708a-4ed7-bd32-f297538dbf19
---
feature = PolynomialFeature(24)
# feature = GaussianFeature(np.linspace(0, 1, 24), 0.1)
# feature = SigmoidalFeature(np.linspace(0, 1, 24), 10)

for a in [1e2, 1., 1e-9]:
    y_list = []
    plt.figure(figsize=(20, 5))
    plt.subplot(1, 2, 1)
    for i in range(100):
        x_train, y_train = create_toy_data(sinusoidal, 25, 0.25)
        X_train = feature.transform(x_train)
        X_test = feature.transform(x_test)
        model = BayesianRegression(alpha=a, beta=1.)
        model.fit(X_train, y_train)
        y = model.predict(X_test)
        y_list.append(y)
        if i < 20:
            plt.plot(x_test, y, c="orange")
    plt.ylim(-1.5, 1.5)
    
    plt.subplot(1, 2, 2)
    plt.plot(x_test, y_test)
    plt.plot(x_test, np.asarray(y_list).mean(axis=0))
    plt.ylim(-1.5, 1.5)
    plt.show()
```

+++ {"id": "qxjO61pe0pdi"}

## 3.3 Bayesian Linear Regression

+++ {"id": "f9bnW8tX0pdi"}

### 3.3.1 Parameter distribution

```{code-cell} ipython3
:id: PJb9V5Wp0pdj
:outputId: 4a056e57-632d-431d-a76d-56fcc6188c0e

def linear(x):
    return -0.3 + 0.5 * x


x_train, y_train = create_toy_data(linear, 20, 0.1, [-1, 1])
x = np.linspace(-1, 1, 100)
w0, w1 = np.meshgrid(
    np.linspace(-1, 1, 100),
    np.linspace(-1, 1, 100))
w = np.array([w0, w1]).transpose(1, 2, 0)

feature = PolynomialFeature(degree=1)
X_train = feature.transform(x_train)
X = feature.transform(x)
model = BayesianRegression(alpha=1., beta=100.)

for begin, end in [[0, 0], [0, 1], [1, 2], [2, 3], [3, 20]]:
    model.fit(X_train[begin: end], y_train[begin: end])
    plt.subplot(1, 2, 1)
    plt.scatter(-0.3, 0.5, s=200, marker="x")
    plt.contour(w0, w1, multivariate_normal.pdf(w, mean=model.w_mean, cov=model.w_cov))
    plt.gca().set_aspect('equal')
    plt.xlabel("$w_0$")
    plt.ylabel("$w_1$")
    plt.title("prior/posterior")

    plt.subplot(1, 2, 2)
    plt.scatter(x_train[:end], y_train[:end], s=100, facecolor="none", edgecolor="steelblue", lw=1)
    plt.plot(x, model.predict(X, sample_size=6), c="orange")
    plt.xlim(-1, 1)
    plt.ylim(-1, 1)
    plt.gca().set_aspect('equal', adjustable='box')
    plt.show()
```

+++ {"id": "xrpTxWaQ0pdm"}

### 3.3.2 Predictive distribution

```{code-cell} ipython3
:id: djlxk9bc0pdm
:outputId: a42f307a-5e81-4209-d66a-3a4a71c79fd1

x_train, y_train = create_toy_data(sinusoidal, 25, 0.25)
x_test = np.linspace(0, 1, 100)
y_test = sinusoidal(x_test)

feature = GaussianFeature(np.linspace(0, 1, 9), 0.1)
X_train = feature.transform(x_train)
X_test = feature.transform(x_test)

model = BayesianRegression(alpha=1e-3, beta=2.)

for begin, end in [[0, 1], [1, 2], [2, 4], [4, 8], [8, 25]]:
    model.fit(X_train[begin: end], y_train[begin: end])
    y, y_std = model.predict(X_test, return_std=True)
    plt.scatter(x_train[:end], y_train[:end], s=100, facecolor="none", edgecolor="steelblue", lw=2)
    plt.plot(x_test, y_test)
    plt.plot(x_test, y)
    plt.fill_between(x_test, y - y_std, y + y_std, color="orange", alpha=0.5)
    plt.xlim(0, 1)
    plt.ylim(-2, 2)
    plt.show()
```

+++ {"id": "J2Va-_K90pdo"}

## 3.5 The Evidence Approximation

```{code-cell} ipython3
:id: L7o0pssp0pdp
:outputId: 60be2ae8-f5e7-4784-9526-ac39c2bdb5fd

def cubic(x):
    return x * (x - 5) * (x + 5)

x_train, y_train = create_toy_data(cubic, 30, 10, [-5, 5])
x_test = np.linspace(-5, 5, 100)
evidences = []
models = []
for i in range(8):
    feature = PolynomialFeature(degree=i)
    X_train = feature.transform(x_train)
    model = EmpiricalBayesRegression(alpha=100., beta=100.)
    model.fit(X_train, y_train, max_iter=100)
    evidences.append(model.log_evidence(X_train, y_train))
    models.append(model)

degree = np.nanargmax(evidences)
regression = models[degree]

X_test = PolynomialFeature(degree=int(degree)).transform(x_test)
y, y_std = regression.predict(X_test, return_std=True)

plt.scatter(x_train, y_train, s=50, facecolor="none", edgecolor="steelblue", label="observation")
plt.plot(x_test, cubic(x_test), label="x(x-5)(x+5)")
plt.plot(x_test, y, label="prediction")
plt.fill_between(x_test, y - y_std, y + y_std, alpha=0.5, label="std", color="orange")
plt.legend()
plt.show()

plt.plot(evidences)
plt.title("Model evidence")
plt.xlabel("degree")
plt.ylabel("log evidence")
plt.show()
```

```{code-cell} ipython3
:id: tSjwpO9r0pdt


```
