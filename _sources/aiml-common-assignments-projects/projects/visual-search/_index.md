---
title: Reverse Visual Search
---

# Reverse Visual Search

In many domains we are interested in finding artifacts that are similar to a query artifact. In this project you are going to implement a system that can find artifacts when the queries are visual.  The type of queries you will test your system on are images of faces (30 points) and videos of people (40 points). You will also document your approach clearly showing advantages over the baseline - the documentation is worth 30 points but to earn them you need to write in the markdown (\*.md) or restructured text (\*.rst) formats. 

In the following we use the term person of interest (PoI) to indicate the person that we reverse search on images and videos. The PoI may be present together with others in the datasets but the system should be able to retrieve the images / videos that the PoI is in all conditions minus complete occlusion of the face.  See bonus points for partial occlusion. 

## Datasets

### Images - LFW Dataset

[This](http://vis-www.cs.umass.edu/lfw/) dataset will be used for images. 

### Videos - YouTube Faces

[This](https://www.cs.tau.ac.il/~wolf/ytfaces/) dataset will be used for videos. We will post an alternative link to a Gdrive download folder in the class slack. For the description of each file please consult the authors' website. 

## Reverse Image Search - Baseline (10 points)

You will use [this](https://aws.amazon.com/blogs/machine-learning/building-a-visual-search-application-with-amazon-sagemaker-and-amazon-es/) reverse image search system as the baseline prototype. We suggest you start here to understand how the baseline system works for faces. AWS has launched recently Opensearch - please select ES when you run the baseline example.  

## Reverse Image Search - Siamese Networks (20 points)

In this step you will need to 

1. Mirror the baseline in terms of workflow. You can use [elasticknn](https://github.com/alexklibisz/elastiknn) - see [here](https://colab.research.google.com/github/tensorflow/io/blob/master/docs/tutorials/elasticsearch.ipynb#scrollTo=Tce3stUlHN0L) how ES can be used inside colab. You can also use [Weaviate](https://www.semi.technology/developers/weaviate/current/index.html) or [Milvus](https://milvus.io/) for similarity search. You will need to beat the baseline above which means that you first need to feed the baseline with LFW data to obtain the baseline performance for LFW. 

2. To improve over the baseline you may want to look at networks such as FaceNet and others quoted [here](https://hackernoon.com/6-best-open-source-projects-for-real-time-face-recognition-vr1w34x5) as well as try various similarity search algorithms. 


## Reverse Video Search (40 points)

Here you will demonstrate that the system is able to produce the videos involving a person of interest from a query video that obviously contains the person of interest. The query video can be one of the videos in the database. 

Note that you may want to work with  [a cleaner version](https://www.kaggle.com/selfishgene/youtube-faces-with-facial-keypoints) of the dataset that uses an alignment library as demonstrated below: 

{{<youtube 8FdSHl4oNIM>}}

Clearly explain your ideas on how best to obtain the embeddings for the query / database videos. Perhaps a straightforward way is to average the per frame embeddings but you can think of other methods. Your notebook must be able to return the videos of the PoI that exists in the database minus the query video.   

## Documentation (30 points)

Remember to document everything - setup instructions written in such a way so that someone else can replicate your experimenents, methods and methodologies, how each method works eg. if you use FaceNet you need to explain Siamese Networks, experiments you made etc. 


