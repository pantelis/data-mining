# Reported.ai - News Aggregation with AI Agents


```{eval-rst}
.. youtube:: wArETCVkS4g
```

The video above helps you understand the end deliverable of this project. You will be working individually to develop the intelligent services needed by a django-based news aggregation site that mines youtube video transcriptions and presents them as news articles. Each one of you will select one of the following areas to work on.


## Django site operation and Integration

The deliverable is the django web site that will display the news and the integration of the components.

1. You will need to bring up [this implementation](https://realpython.com/build-a-content-aggregator-python/) 
2. Write the elements of the code that will subscribe to Kafka events such as [this](https://github.com/addu390/django-kafka). Please note that you can implement Kafka via [Redpanda](https://redpanda.com/). 
3. Ensure that the site is operational and can integrate in the intelligent services.

## Recommendation System

1. You will be building a recommendation system that recommends transcribed video content to all of the twitter topic categories. You will select 10 Twitter users (real people, not organizations) and determine which of the youtube transcriptions you need to feed the app for each one of them.  Your recommendations will be based on their past retweets so select people that are very active on twitter. 

2. The output should be published into kafka topics and stored in an Elastic Search server. 
   

## Transcription Retrieval and Summarization

1. You will be using the youtube data api to retrieve the transcriptions from each of the videos in the stream. 

2. You will store the transcription and summarize it using existing NLP models for text summarization. 

3. You will publish the transcription and summary in Kafka topics.  

## Semantic Search

1. You will be subscribe to transcription Kafka topics and  encode each transcription summary into a vector (embedding). See [this artcle](https://medium.com/version-1/vector-based-semantic-search-using-elasticsearch-48d7167b38f5) on how to do that in Elastic Search. 

2. You will be offering via the django app the ability to the users to perform the semantic search and retrieve relevant transcriptions to keyword queries.




