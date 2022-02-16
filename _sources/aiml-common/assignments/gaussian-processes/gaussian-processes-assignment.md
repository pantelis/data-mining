---
title: Bayesian Optimization Assignment
---

In this assignment you are asked to study Gaussian Processes  as applied to Bayesian Optimization that is currently considered the cutting edge amongst hyperparameter optimization methods. 

1. (10 points) Learn the fundamentals of GPs e.g. from [here](https://distill.pub/2019/visual-exploration-gaussian-processes/) and the references therein e.g. [this one](https://peterroelants.github.io/posts/gaussian-process-tutorial/). 

2. (20 points) See [this](https://ax.dev/docs/bayesopt) tutorial and use BOTorch to do [Bayesian Optimization](https://arxiv.org/abs/1206.2944) of the hyperparameters of the [Yolact++](https://arxiv.org/abs/1912.06218) with ResNet-101 feature extraction network for a semantic segmentation use case that will be given to you. When you execute this step, you will be provided with a docker container and data for this use case. 


## Extra credit (5 points)

Prototype the assignment as an [executable book](https://jupyterbook.org/intro.html) and publish it on Github pages. This will serve the proof of concept for the course site itself to be migrated to a `jupyterbook` format. 