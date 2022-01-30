---
title: Big Transfer
---
(project:big-transfer)=
# Big Transfer 

In this project you will look at a general representation learning method called [Big Transfer](https://arxiv.org/pdf/1912.11370.pdf) that was found that is particularly good in specialized small label downstream tasks. 

> (from the abstract) Transfer of pre-trained representations improves sample efficiency and simplifies hyperparameter tuning when training deep neural
networks for vision. We revisit the paradigm of pre-training on large supervised datasets and fine-tuning the model on a target task. We scale
up pre-training, and propose a simple recipe where by combining a few carefully selected components, and transferring using a simple heuristic, we achieve strong performance on over 20 datasets.

```{eval-rst}
.. youtube:: k1GOF2jmX7c
```

## Tasks

1. Write a 2 page (excluding pictures) summary of what is transfer learning. (10 points)
2. Write a 2 page (excluding pictures) summary of what architectural improvements, if any, the authors have assumed on top the ResNet-xyz V1  architecture and why. (20 points)
3. Write a 4 page (excluding figures) summary of the key points that need to be made so a non-expert can understand the differences between Group Normalization (GN), Weight Standardization (WS) and Batch Normalization (BN). (30 points)
4. Write a 2 page (excluding figures) summary of MixUp regularization and how this may help. (20 points) 
5. Apply the Big Transfer technique from [this repo](https://github.com/google-research/big_transfer) in CIFAR10 downstream dataset for 1-10 examples per class (low-data regime). Match the behavior of Fig 6 of the paper for one upstream dataset of your choice and ResNet50-x3 architecture. (20 points) 

## Notes:

1. You are free to select your computing  environment but a default choice is Google Colab. We have confirmed that the notebooks in the repo are running successfully in Colab. 




