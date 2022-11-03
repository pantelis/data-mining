# Reverse Visual Search

![](coco.png)

In many domains we are interested in finding artifacts that are similar to a query artifact. In this assignment you are going to implement a system that can find artifacts when the queries are visual. 

The type of queries you will test your system on are MS COCO dataset images.


## Dataset (10 points)

Your images will be from the [MSCOCO mini dataset](https://github.com/giddyyupp/coco-minitrain) and will be of class `person`. Download the dataset to your Gdrive. 

## Pretrained Object Detection  (30 points)

Using a model pretrained to perform object detection on MS COCO (e.g. https://pytorch.org/vision/stable/models/faster_rcnn.html ) extract the bounding boxes of all people in your dataset. List details of the object detector used and code the pipeline that results in the required inference json file. 

## Reverse Image Search - Feature extraction (30 points)

See [this example](https://aws.amazon.com/blogs/machine-learning/building-a-visual-search-application-with-amazon-sagemaker-and-amazon-es/) on how AWS is suggesting to build a reverse image search system.

Using eg. ResNet-50 as a featurizer (ensure that is the featurizer used by the object detector), extract for each detected bounding box the representation vector (2048 elements long).

## Reverse Image Search - Similarity Search  (30 points)

Using five (5) of the person bounding boxes  as query, pick a [similarity search python library](https://github.com/currentslab/awesome-vector-search) to return the 10 most similar bounded boxed persons to the query image. 

Before you can execute the similarity search, you may have to do dimensionality reduction - clearly explain how you did that.


Select carefully the query image so that the results can be revealing of the ability of your representation and the search engine. 

Remember to document everything - setup instructions written in such a way so that someone else can replicate your assignment. You deliver this assignment as a Github URL and notebooks and/or markdown files should contain all the results. 
