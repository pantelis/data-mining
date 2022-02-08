---
title: Graph Embeddings
---

# Graph Embeddings

## Motivating use case

"A government client wanted to perform flexible similarity driven search and outlier detection in cybersecurity data, where network entities (e.g., routers, computers, processes, files, IP addresses) and their relationships (e.g., a process opened a file, or a connection to a local machine was opened from a remote IP address) are represented as very large graphs.  The goal was to support queries like “show more more processes like this one” or “show me IP addresses with unusual behavior”. The difficulty is that computing similarity between sub-graphs is computationally very expensive, and may not capture structure that is important for this specific task." Retrieved from [synaptiq](https://www.synaptiq.ai/deep-machine-learning-applied-to-cybersecurity-graphs/)

## The Node-embedding goal

Assume that we have an input graph $G=(V,E)$. 

![graph-embedding](images/goal-graph-embedding.png)

The goal of graph embedding is to embed the nodes of the graph in a vector space (encoding process) such that two nodes that are dependent (e.g. connected, share neighbors, etc.) on each other in the graph space, appear in the embedding space as vectors that possess strong similarity according to a metric. In other words, we are after the coordinates of the vectors in the embedding space that preserve the similarity evident in the graph space.  

More explicitly we need to specify three things:

![encoder-goal](images/encoder-goal.png)

![encoder-goal2](images/encoder-goal-2.png)

## Encoder Design

The encoder function is a LUT with each row being the node graph index and the d-dim embedding of that node ($\mathbf z_v$)

![encoder-lut](images/encoder-lut.png)

![encoder-lut-2](images/encoder-lut-2.png)

## Similarity

### Random Walks on Graphs


![random-walk-example](images/random-walk-example.png)
_Random walk example_


### DeepWalk Embeddings


![random-walk-similarity](images/random-walk-similarity.png)

![random-walk-similarity-2](images/random-walk-similarity-2.png)

Why random walks are useful abstraction mechanisms? First, they provide the flexibility of a stochastic definition of node similarity that incorporates both local and higher-order neighborhood information. Second, during training we not need to consider all node pairs; only need to consider pairs that co-occur on random walks. 

####  Deepwalk Objective

![deepwalk-objective](images/deepwalk-objective.png)

#### Deep walk method

![deep-walk-method](images/deep-walk-method.png)

#### Likelihood parameterization

![likelihood-parameterisation](images/likelihood-parameterisation.png)

![minimizing-loss-deepwalk](images/minimizing-loss-deepwalk.png)










