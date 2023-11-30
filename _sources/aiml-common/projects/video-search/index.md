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

Combine the video embeddings into a single vector using a method of your choice that includes simple aggregation of the per-frame embeddings.

#### Extra credit
Extra credit: if you want to maximize the possibility of developing something **new** think how a simple aggregation can be replaced by a more complex function. For example, [in this ~3min video accessed Nov 2023](https://youtu.be/FN8a8mZNik8?si=wXdbOGuLGkGsWsf) you have multiple scenes each one lasting 30sec or so. Can you find a way to segment each video and aggregate the frame embeddings of each segment ?  This way there are multiple embeddings per video and you need to keep them that way for the subsequesnt steps of this project.

### Indexing

Use `docker compose` to bring up two docker containers, your application container with the dev environment (you must have done this in Milestone 1) and a second container with either postgres or OpenSearch. Its entirely up to you to decide which database to use.

`docker pull postgres:latest`
`docker pull opensearchproject/opensearch:latest`

Index the video images embedding vectors in the database of your choice. To do that in postgres (with the pgvector extension) you can use [this guide](https://dev.to/sfoteini/image-vector-similarity-search-with-azure-computer-vision-and-postgresql-12f7). To do that in OpenSearch you can use [this guide](https://opensearch.org/docs/latest/knn-search/) and [this guide](https://dev.to/finloop/how-to-use-opensearch-k-nn-as-a-semantic-search-engine-je9).

Demonstrate that you can search the database using image queries and post the screenshots of your search results that must include the first 10 similar images across the input videos. 


## Milestone 3: Text indexing pipeline (25 points)

The youtube service give you the ability of downloading the closed captions of a video. You can do that by clicking on the three dots on the bottom right of the video and then clicking on the "Open transcript" option. 

Implement the text embeddings as described in Fig 4.13-4.15.  You can only use word2vec or transformers-based models. Word2vec embeddings are the simplest to implement and you can use the [gensim](https://radimrehurek.com/gensim/) library to do that. You can use the [Hugging Face Hub](https://huggingface.co/) to download the pretrained models you decided to use. [Gensim has published some](https://huggingface.co/models?other=gensim) models that you can use.

Index the text embeddings in the database of your choice. You can use the Milestone 2 links to do so. 


## Milestone 4: Fusion of nearest videos and text (25 points)

You can now implement Fig 4.18 where you will form the dot products of the video and text embeddings and you will train a model that has been used to retrieve images of the Flickr-8k dataset from  natural language descriptions (captions).  

### Projection head (5 points)

In this subtask you need to implement the transformation of the image and the text embeddings to the same embedding space with the same dimensionality. You can see the implementation for Keras of the projection head [here](https://keras.io/examples/vision/nl_image_search/). It is implemented using Dense layers and you can easily recode to a Pytorch implementation. 

### Contrastive loss (5 points)

Implement the learning approach using contrastive loss as described [here](https://towardsdatascience.com/understanding-contrastive-learning-d5b19fd96607). You need to excessively document the code of the implementation shown [here](https://keras.io/examples/vision/nl_image_search/) to win any points in this milestone. 

### Train the model (15 points)

Download the Flickr-8k dataset from [here](https://www.kaggle.com/adityajn105/flickr8k?select=Flickr_Data). You use the [Flickr8k_Dataset](https://www.kaggle.com/adityajn105/flickr8k?select=Flickr_Data) and [Flickr8k_text](https://www.kaggle.com/adityajn105/flickr8k?select=Flickr_Data) folders.

Plot the train and validation loss function as the model trains (vs epochs). Note that the end to end model training will require you to reuse the embedding functions you have developed in earlier milestones. 

## Milestone 5: Search UI and  pitch video voiceover (15 points)

You developed a model that retrieves relevant to the text query images using the Flickr8k dataset and you will now use the model for video retrieval. Since the video and trascription are just vectors the approach will work.  Exercise the model and create a UI similar to [this one](https://huggingface.co/spaces/keras-io/dual-encoder-image-search) that will allow you to search for the NPR news videos using natural language. You can use the [Hugging Face spaces](https://huggingface.co/spaces) to deploy your model and host your UI that is easily coded using [https://www.gradio.app/]. 

