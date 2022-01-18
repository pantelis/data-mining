---
title: Syllabus
weight: 10
draft: false
---
# Syllabus

## Books

There are three axes that data mining intersects: data, methods and systems. 

**Data & Methods-oriented books:**

* Main textbook on ML methods: _"Hands-On Machine Learning with Scikit-Learn, Keras, and TensorFlow"_, 2nd Edition, by Aurélien Géron, 2019. [Amazon](https://www.amazon.com/Hands-Machine-Learning-Scikit-Learn-TensorFlow/dp/1492032646/ref=dp_ob_title_bk) This book will be referred to as `GERON` in the syllabus. 
 
* Supplemental book on data methods that are not covered by Geron's book: "Mining of Massive Datasets" by Jure Leskovec, Anand Rajaraman, Jeff Ullman. [Free download](http://infolab.stanford.edu/~ullman/mmds/bookL.pdf). This book will be referred to as `ULLMAN` in this syllabus 

**Systems-oriented books:**

* Supplemental free book to provide additional input for the engineering / applied aspects of data mining and machine learning today: [_ML Engineering_](http://www.mlebook.com/wiki/doku.php), by Andriy Burkov, 2020. Note that the free draft pdf files are at the end of the page. 

* Optional book on data-driven application architectures: _"Designing Data-Intensive Applications: The Big Ideas Behind Reliable, Scalable, and Maintainable Systems"_, by Martin Kleppmann,   [Amazon](https://www.amazon.com/Designing-Data-Intensive-Applications-Reliable-Maintainable/dp/1449373321)
## Schedule


| Lecture |  Description | Reading List | 
| ------- | ---- | --- | 
| 1       | We start with an _introduction to data mining_ and through an end to end data mining application we understand and experience in our Colab notebooks all the stages of a data mining pipeline. At the same time we (a) review essential Python language coding skills,  set up of your computing environment that you need to complete this course and (b)  review elements of probability and statistics necessary for the remainder of the course. | GERON Chapter 1 |
|  2  | Almost all the tasks you will be called to perform as data scientists and analysts will have a flavor of  _supervised learning_. Here we start with this learning problem for regression.  | GERON Chapter2 | 
|  3  | Staying at supervised learning, we will learn how to (a) pose the Maximum Likelihood Estimation (MLE) problem that optimizes the parameters (b) solve the MLE via an algorithm that is the workhorse of modern machine learning: the _stochastic gradient descent_.  | GERON Chapter 4 |
|  4  |  We continue with classical classification algorithms and learn how to interpret key performance metrics that arise in such problems. |  GERON Chapter 3 |
| 5.1 |  _Decision Trees_ are probably the most versatile and extensively used tools for data mining. We start with a review of entropy and deep dive on how they work.  | GERON Chapter 6  |
| 5.2  |  _Random Forests_  and in general _Ensemble Methods_ are a natural conceptual extension of decision trees. They can still handle massive datasets _and_ offer partially _explainable_ decisions.  | GERON Chapter 7   | 
| 6  | **Good luck in your Midterm**  | | 
| 7   | We now expand into _Deep neural networks_ that are developed bottom up from the perceptron algorithm and logistic regression. We use the Tensorflow playground to understand the tradeoffs between classical and deep architectures and why deep neural networks dominate in unstructured big data applications today.  | GERON Chapter 10   | 
| 8  | We review one of the most popular DNN architectures in use today: CNNs. They are instrumental to tasks involving feature extraction from images / video. | GERON Chapter 14  |
| 9 | We now expand to methods that predict on data sequences. We present Recurrent Neural Networks (RNNs) that are heavily used to predict time series data and generate embeddings in natural language processing (NLP). | GERON Chapter 15 |  
| 10  | What happens if training data are not available or very expensive to acquire ? This week we review unsupervised learning and _clustering_ approaches such as K-means. We review use cases in anomaly and novelty detection. | GERON Chapter 9  and ULLMAN Chapter  7  |
| 11 | What about if we are dealing with neither a classification or regression task ? A common task is matching also known as _similarity search_.  Face recognition applications for example use many of the methods we already discussed but at the end they need to return the closest to the query (person of interest)  set of images recorded in a video surveillance system. We will discuss _approximate nearest neighbors_ techniques such as  Locally Sensitive Hashing (LSH) and their implementation in Facebook AI Similarity Search (FAISS) or other similar systems. | ULLMAN Chapter 3 | 
| 12 | Graph and many other representations of a structured data problem, lead to tall or fat data matrices of high dimensionality. _Dimensionality Reduction_ is commonly applied to improve significantly the signal to noise ratio. | GERON Chapter 8 |
| 13   | _State of the Art Systems_   We close by looking a cloud computing and reviewing the tools and ways of working that you as data scientists need to be familiar with to build data-intensive applications. | GERON Chapter 19 and Notes | 
| 14      | This is a review lecture before the final.  It also acts as a buffer in case we run late. | | 
| 15    | **Good luck in your final**         |  | 
## Projects

Project details will be published soon. 

<!-- For details on 3 projects that you need to submit see [Projects](../projects/_index.md) page - projects are published after the semester starts.  -->
