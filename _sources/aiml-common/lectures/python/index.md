
# Learn Python

Below is a list of recommended resources that will teach you quickly Python. You can select the right format based on your own experience on how best you learn. No matter what you do there is a good Python book to help you and use as a reference:  _Think Python by Allen B. Downey, 2nd edition_. This is an open source book. It is available without charge in HTML and PDF formats at http://greenteapress.com/wp/think-python-2e/ (Links to an external site.).

## Basic Python

Harvard's CS50p is the most popular way to learn basic Python. Accessible [here](https://cs50.harvard.edu/python/2022/) and in edX. 


## Python and Data Science 

The following are your options with 1 being the highest priority. 

1. IBM's [Python Basics for Data Science](https://www.edx.org/course/python-basics-for-data-science)

2. [Kaggle Python Course](https://www.kaggle.com/learn/python)

3. [CodeAcademy Data Science Path](https://www.codecademy.com/learn/paths/data-science). Take Python modules 4-10. This course introduces Numpy and Panda as well. 


## General computational Python libraries

1. [Numpy Tutorial - Stanford's CS231n](http://cs231n.github.io/python-numpy-tutorial/). This [Numpy Cheatsheet](https://s3.amazonaws.com/assets.datacamp.com/blog_assets/Numpy_Python_Cheat_Sheet.pdf) may be useful as well.

2. This is the "official" documentation on Pandas:  [Pandas: powerful Python data analysis toolkit](https://pandas.pydata.org/pandas-docs/stable/pandas.pdf)

3. For many computational problems you may need to use constructs that need compute acceleration such as GPUs, TPUs etc.  Pytorch is a Python package that provides two high-level features: 

    - Tensor computation (like NumPy) with strong GPU acceleration
    - Deep Neural Networks built on a tape-based autograd system

    Many practitioners use Pytorch to prototype a from-scratch implementations and understand how a new concept works without necessarily using the clases and functions provided by the library. This way Pytorch is similar to JAX albeit without the benefits (but also the constraints) of functional programming that JAX provides. In addition, [`torch.func`](https://pytorch.org/blog/pytorch-2.0-release/#stable-features) will also offer a JAX-like API for Pytorch. Since Pytorch is more popular than JAX and is used in many production systems as of the time of the writting of this book, we recommend new learners to start with Pytorch after learning the basics of numpy. 

4. JAX is an extensible system for **composable function transformations** and offers a numpy-like API and can run your code much faster. You can read its benefits for a wide range of scientific applications [here](https://github.com/google/jax). JAX has been extended with NN libraries such as [Equinox](https://github.com/patrick-kidger/equinox) but can also be used without any NN libraries to build for example differentiable physics simulators and other computational applications. 


```{eval-rst}
.. youtube:: WdTeDXsOSj4
```

## Preparing for an interview

[Leetcode](https://leetcode.com/) is perhaps the most popular destination for anyone that wishes to use the skills learned here to launch a software development career in tech. It helps you answer all coding-based interview questions. 