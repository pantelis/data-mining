---
title: Continual Learning 
---

# Continual Learning (CL) 

In this project you will implement continual learning and you are _free to select a method_ from any of these three non-exclusive categories, [as described in detail](https://arxiv.org/abs/1802.07569). This is a very active research area and you will find the starting repo in the [CVPR-2020 competition page](https://sites.google.com/view/clvision2020/challenge?authuser=0). Please pay attention to the paragraph "Challenge Repository" that is replicated below:

```{admonition}
The official starting repository for the CVPR-2020 CLVision challenge con *Continual Learning for Computer Vision* can be found [here](https://www.google.com/url?q=https%3A%2F%2Fgithub.com%2Fvlomonaco%2Fcvpr_clvision_challenge&sa=D&sntz=1&usg=AFQjCNEEXzPuBUcsp0QyxsVfB97SGD2r2w) and it contains:

Two scripts to setup the environment and generate the zip submission file.
A complete working example to: 1) load the data and setting up the continual learning protocols; 2) collect all the metadata during training 3) evaluate the trained model on the valid and test sets.
Starting Dockerfile to simplify the final submission at the end of the first phase.
```

## Datasets and Tasks

![core50](images/core50.gif)

You are given two dataset options for this project as shown in the table below. The CORe50 option is more difficult than the MNIST option. Grading will happen relative to teams that selected the same option. The CORe50 option may require AWS GPU resources to run. MNIST is able to run in Colab with standard free accounts. If you have access to compute, you will learn more from selecting the CORe50 option as this is closest to a real life dataset than the rotated MNIST which is not even testing for new classes - rather it tests CL on rotated version of classes it has seen before.

| CORe50 Option                                                                                                                    | Rotated MNIST Option                                                                                                                                                                                     |
| -------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| You will use [this](https://vlomonaco.github.io/core50/index.html) dataset and evaluate your method for New Class (NC) scenario. | Use the dataset provided [here](https://github.com/facebookresearch/GradientEpisodicMemory)  based on [this paper](http://papers.nips.cc/paper/7225-gradient-episodic-memory-for-continual-learning.pdf) |
| Object recognition (classification).                                                                                             | Object recognition (classification).                                                                                                                                                                     |

## Methods with repos

Below is a list of repos implementing CL methods - you may consider them for your submission but are _not_ vetted by the instructor.  

| Method | Repo                                                       |
| ------ | ---------------------------------------------------------- |
| EWC    | https://github.com/kuc2477/pytorch-ewc                     |
| GEM    | https://github.com/facebookresearch/GradientEpisodicMemory |