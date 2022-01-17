---
title: CNN Explainers
---

# CNN Explainers 

## Visualising the CNN internals and what they pay attention to

Given the 'black box' nature of CNNs, we need to be familiar with the tooling needed to visualize their internal representations. 

{{<hint info>}}
You must run step by step the notebook below to fully understand what kind of transformations the convolutional layers are performing. It uses simple as well as VGG16 networks. 
{{</hint>}}

<iframe src="https://nbviewer.jupyter.org/github/pantelis/deep-learning-with-python-notebooks/blob/master/5.4-visualizing-what-convnets-learn.ipynb" width="900" height="1200"></iframe>


## Grad-CAM

One of the most popular visualization methods is the Gradient weighted Class Activation Mapping ([Grad-CAM](http://gradcam.cloudcv.org/)) that uses the class-specific gradient information flowing into the final convolutional layer of a CNN to produce a coarse localization map of the important regions in the image. 

![gradcam](images/gradcam.png)
_GradCAM block diagram_

![gradcam-result](images/gradcam-result.png)
[_Results of GradCAM_](https://www.kaggle.com/nguyenhoa/dog-cat-classifier-gradcam-with-tensorflow-2-0) _for ResNet50 training on ImageNet_

## Occlusion Sensitivity

In most instances we need to have an evaluation of robustness of a CNN to occlusions. This is quite important for video surveillance systems.  To achieve that, we mask a part of the image (using a small square patch placed randomly) and observe if the prediction is still correct, on average, the network is robust. The area in the image that is the warmest (i.e., red) has the most effect on the prediction when occluded as shown below.

![gradcam-occlusion-sensitivity](images/gradcam-occlusion-sensitivity.png)
_Occlusion Sensitivity_



## Grad-CAM Demonstration

The Grad-CAM has been implemented in tf-explain APIs and is readily available to use. Se also [other writeups](https://www.pyimagesearch.com/2020/03/09/grad-cam-visualize-class-activation-maps-with-keras-tensorflow-and-deep-learning/) that demonstrate its usage in helping us design better / more robust CNNs. 

NOTE: Click [here](https://github.com/PracticalDL/Practical-Deep-Learning-Book/blob/master/code/chapter-2/2-colab-what-does-my-neural-network-think.ipynb) to view if the notebook below is not visible in Github pages.

<iframe src="https://github.com/PracticalDL/Practical-Deep-Learning-Book/blob/master/code/chapter-2/2-colab-what-does-my-neural-network-think.ipynb" width="900" height="1200"></iframe>
