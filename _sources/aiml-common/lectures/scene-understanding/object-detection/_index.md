---
title: Object Detection
weight: 73
draft: false
---

# Object Detection

In the introductory section, we have seen examples of what object detection is. In this section we will treat the detection _pipeline_ itself, summarized below:

![object-detection-e2e](images/object-detection-e2e.png)
*Object detection pipeline*. 

Work on object detection spans 20 years and is impossible to cover every algorithmic approach in this section - the interested reader can trace these developments by reading in [this](https://arxiv.org/abs/1905.05055) paper. 

![object-detection-roadmap](images/object-detection-roadmap.png)

As expected, since 2014, deep learning has surpassed classical ML in the detection competitions - we therefore focus only on such architectures. More specifically we will be focusing on the so called _two stage_ detectors that employ two key ingredients: 

1. Recognition using _regions_. 
2. CNNs. 

Object detection, involves three main stages: the feature extraction stage, the classification stage and the detection or localization stage. In the literature the feature and classification stages are counted as one, called the classification stage and people refer to such architecture as _two stage. 

We also need to insert an additional requirement: to be able to detect objects in almost real time (20 frames per second) - a significant subset of what we call mission critical applications require it. Therefore will focus a specific family that is considered to be the canonical CNN architecture for detection - the family of Region CNNs.  

