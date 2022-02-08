---
title: The Zillow App
weight: 210
---

# The Zillow App

The Zillow app is based on the end to end machine learning example from Chapter 2 of [Hands-On Machine Learning with Scikit-Learn, Keras, and TensorFlow, 2nd Edition](https://learning.oreilly.com/library/view/hands-on-machine-learning/9781492032632/ch02.html). If you dont have this book, there is no need to worry as the code is freely available in Github.  

The usual eight steps of the data and model training pipeline as shown below. 

![simple-workflow](images/simple-workflow.png)
*High level view of house pricing pipeline stages*

> As discussed the data pipeline is responsible for providing the training datasets if the aim is to train (or retrain) a model. For the purposes of this lecture we assume that we deal with *small data* aka. data fit in the memory of today's typical workstations/laptops (< 16 GB).  Therefore you will be given a URL from where compressed data files can be downloaded.  For structured data, these files when uncompressed will be typically CSV. For unstructured they will be in various formats depending on the use case. In most instances, ML frameworks that implement training will require certain transformations to optimize the format for the framework at hand (e.g. [TFrecords](https://www.tensorflow.org/tutorials/load_data/tfrecord)).  

During the class we will go through [notebook 2](https://github.com/ageron/handson-ml2/blob/master/02_end_to_end_machine_learning_project.ipynb). You just click the Open in Colab icon to load it to your Colab environment but it is highly recommended to fork the repo as described in the development environmen section. 

We are going to go critically through the code, asking questions such as those below (far more will be asked during the lecture) but not before creating a topological map of code to pipeline stage in our minds. 

1. Is the dataset appropriate for training?

![California-housing-histograms](images/california-housing-histograms.png)

> Any unexpected ranges, any range heterogeneity, any clipping?
> 
> Do we face long-tails?
> 
> What options do we have to glean the data?

2. What will happen if we remove the following line from the ```split_train_set``` function?
 
    ```python
    shuffled_indices = np.random.permutation(len(data))
    ```
