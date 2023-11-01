# Youtube Video Search

See Discord group for project description.

## Milestone 1:  youtube video library (10 points)

Write a python API  that will download the video and its closed captions from youtube.

Your library will consist of 50 videos (approx 3min each) of th [NPR youtube channel](https://www.youtube.com/@NPR/videos). Write python code to download the source videos and their transcriptions into a Gdrive dir. You can collaborate with other teams to share the workload and create a common library of videos and transcriptions to save time. Your team can contribute a handful of videos to the shared folder [here](https://drive.google.com/drive/folders/1VV2B00opRoBaao7ReuYwvkeX_mnpcMk8?usp=share_link). 

## Milestone 2: Video indexing pipeline (25 points)

In this milestone you will start delivering features that will be used in the final search engine.

### Preprocess of the video

You can use opencv, ffmpeg, gstreameer, https://pytorchvideo.org/ or any other library to implement the preprocessing steps of Fig 4.17 as shown in Fig 4.9.

### Embedding model 

Develop a convolutional autoencoder such as [the one described here](https://blog.keras.io/building-autoencoders-in-keras.html) to create per frame embeddings. You can select to downsample the frame rate.  The end result are pairs of (image, correspodning vector embedding) for each video. You have to store them in [Github LFS](https://docs.github.com/en/repositories/working-with-files/managing-large-files/about-large-files-on-github).  

PS: You can also use [ViT](https://huggingface.co/docs/transformers/model_doc/vit) for the autoencoding function if you want to be more cutting edge. 

### Combination

Combine the video embeddings into a single vector using a methiod of your choice that includes simple aggregation of the per-frame embeddings.

Extra credit: if you want to maximize the possibility of developing something **new** think how a simple aggregation can be replaced by a more complex function. For example can you find a way to segment each video and agre  

### Indexing

Use `docker compose` to bring up two docker containers, your application container with the dev environment (you must have done this in Milestone 1) and a second container with either postgres or OpenSearch. Its entirely up to you to decide which database to use.

`docker pull postgres:latest`
`docker pull opensearchproject/opensearch:latest`

Index the video images embedding vectors in the database of your choice. To do that in postgres (with the pgvector extension) you can use [this guide](https://dev.to/sfoteini/image-vector-similarity-search-with-azure-computer-vision-and-postgresql-12f7). To do that in OpenSearch you can use [this guide](https://opensearch.org/docs/latest/knn-search/) and [this guide](https://dev.to/finloop/how-to-use-opensearch-k-nn-as-a-semantic-search-engine-je9).

Demonstrate that you can search the database using image queries and post the screenshots of your search results that must include the first 10 similar images across the input videos. 


## Milestone 3: Text indexing pipeline (25 points)


## Milestone 4: Fusion of nearest videos and text (20 points)

## Milestone 5: Search UI and  pitch video voiceover (20 points)



