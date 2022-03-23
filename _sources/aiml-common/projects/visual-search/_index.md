---
title: Reverse Visual Search
---

# Reverse Visual Search

In many domains we are interested in finding artifacts that are similar to a query artifact. In this project you are going to implement a system that can find artifacts when the queries are visual.  The type of queries you will test your system on are images of faces (30 points) and videos of people. You will also document your approach clearly showing advantages over the baseline. 

In the following we use the term person of interest (PoI) to indicate the person that we reverse search on images and videos. The PoI may be present together with others in the datasets but the system should be able to retrieve the images / videos that the PoI.  See bonus points for partial occlusion. 

## LFW Dataset (0 points)

[This](http://vis-www.cs.umass.edu/lfw/) dataset will be used for images. 

## Reverse Image Search - Baseline (30 points)

You will use [this](https://aws.amazon.com/blogs/machine-learning/building-a-visual-search-application-with-amazon-sagemaker-and-amazon-es/) reverse image search system as an example system that you will replicate its functionality using libraries. Please do not use the AWS managed  services detailed in this system as you will exhaust your AWS credits. At the end of this task you have documented the components of a reverse image search system and have implemented a baseline system for faces that will be used to obtain a **baseline performance for LFW**. 

## Reverse Image Search Improvement (30 points)

In this step you will need to: 

1. Work inside a Deep Learning AMI Virtual Machine to deploy ES [elasticknn](https://github.com/alexklibisz/elastiknn) [Weaviate](https://www.semi.technology/developers/weaviate/current/index.html) or [Milvus](https://milvus.io/). See for example [here](https://colab.research.google.com/github/tensorflow/io/blob/master/docs/tutorials/elasticsearch.ipynb#scrollTo=Tce3stUlHN0L) how ES can be used with python. 

2. You will need to beat the baseline performance you obtained earlier. To improve over the baseline you may want to look at networks such as FaceNet and others quoted [here](https://hackernoon.com/6-best-open-source-projects-for-real-time-face-recognition-vr1w34x5) as well as try various similarity search algorithms.

## Documentation (40 points)

Remember to document everything - setup instructions written in such a way so that someone else can replicate your experiments, methods and methodologies, how each method works eg. if you use FaceNet you need to explain Siamese Networks, experiments you made, explain the similarity search method you used etc. 

## Extra Credit: Reverse Video Search (20 points)

### Videos - YouTube Faces

[This](https://www.cs.tau.ac.il/~wolf/ytfaces/) dataset will be used for videos. We will post an alternative link to a Gdrive download folder in the class slack. Please do not publish this link anywhere as we need to respect the dataset authors' restrictions. For the description of each file please consult the dataset website. 

### Similarity Search

Here you will demonstrate that the system is able to produce the videos involving a person of interest from a query video that obviously contains the person of interest. The query video can be one of the videos in the database. 

Note that you may want to work with  [a cleaner version](https://www.kaggle.com/selfishgene/youtube-faces-with-facial-keypoints) of the dataset that uses an alignment library as demonstrated below: 

{{<youtube 8FdSHl4oNIM>}}

Clearly explain your ideas on how best to obtain the embeddings for the query / database videos. Perhaps a straightforward way is to average the per frame embeddings but you can think of other methods. Your notebook must be able to return the videos of the person of interest that exists in the database (other than the query video). Ideas that can address problems with partial occlusions are also welcomed. 
