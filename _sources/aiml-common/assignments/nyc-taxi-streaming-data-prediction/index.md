# Online Ensemble Learning from NYC Taxi Ride Event Streams

![](images/header.png)

## Introduction

This is a challenging assignment that requires you to build a streaming data predictor based on an event stream that corresponds to NYC taxi rides.  

The system consists of several components and your job is to implement them in your docker-based development environment as indicatyed in the next steps.


## Task 1: Event simulator

You will build an a publisher that simulates taxi ride events. The publisher will publish events to a [nats.io jetstream server](https://docs.nats.io/nats-concepts/jetstream). Jetstream is used here instead of Apache Kafka as it is engineered to be easier to manage and more efficient (it is implemented in Go). You will use your existing `docker compose` based environment and add to it a single instance of a [jetstream server in the form of a docker service](https://docs.nats.io/running-a-nats-service/nats_docker/jetstream_docker). Please note that you will need to add the jetstream server to your `docker-compose.yml` file and configure it to use a local volume for persistence. 

Events will be published to the `taxi-ride` subject and will be in the form of a JSON object with the following fields:

- `ride_id`: a unique identifier for the ride
- `timestamp`: the time the ride started
- `pickup_longitude`: the longitude of the pickup location
- `pickup_latitude`: the latitude of the pickup location
- `dropoff_longitude`: the longitude of the dropoff location
- `dropoff_latitude`: the latitude of the dropoff location
- `passenger_count`: the number of passengers
- `fare_amount`: the fare amount

Define a docker container called `app` that will host the publisher (also called producer). The publisher will publish events at a rate of $k$ events per second - adjust $k$ to your hardware so that you dont wait too long and face any issues in consuming the events. The events will be generated using the `random` module in Python. The publisher will run as a separate docker service and will be implemented in Python. The publisher will be implemented as a Python script that uses the `nats` library to connect to the jetstream server and publish events to the `taxi-ride` subject.

To implement the publisher, you will need to:

1. Use Dagster to create a pipeline that will convert the csv file to parquet that will be your required data asset. The csv files you will use are available from executing the `kaggle competitions download -c new-york-city-taxi-fare-prediction` command or downloading the data from [here](https://www.kaggle.com/competitions/new-york-city-taxi-fare-prediction/data). 
2. Store each parquet file as a dataset in Hugging Face's Datasets. You can use the `datasets` library do so.
3. Write the publisher that will read from the parquet file and publish the events to the jetstream server. 
 
## Task 2: Event consumer

You need to [implement the event consumer](https://docs.nats.io/nats-concepts/jetstream/consumers/example_configuration) that asynchronously will receive the events and store them into an in-memory database. See the next task for the details of the in-memory database. Your event consumer can be hosted in the same container (`app`) as the producer with the understanding that in a real event streaming system, the producer will not exist and the consumer will be the only component that will be running.

## Task 3: In-memory Database

You will need to store the events in an OLAP database that for this assignment will be [DuckDB](https://duckdb.org/docs/installation/index?version=latest&environment=python). You will host DuckDB in the container `app`. Please note that you need to define a [volume mapping](https://docs.docker.com/storage/volumes/) so your database file is persisted and you dont need to start from scratch if your docker container exited. You will also need to create a table in the database to store the events. The table will have the same fields as the JSON object that defined the trip event earlier.

## Task 4: Incremental vs Batch Learning

We are now ready to start our main objective which is to predict fares of taxi rides. We used the DuckDB facility to allow us to compare between batch and incremental learning on one hands but also to avoid the situation where we have to repeat the event simulation, publication and consumption all over again in case of a temp pipeline failure or during development. 

In a nutshell we will be reading data out of the DuckDB database and train a model that will predict the fare amount of a taxi ride for taxi rides that were never seen in the stream aka they were never stored in DuckDB. Alternatively, you can carve out the validation dataset from DuckDB and you need to explicitly quote what kind of measures you have taken during model training to never consult these rows. 

You will use the [`xgboost` library](https://xgboost.readthedocs.io/en/stable/) to implement a sequential method where 10000 events (rows) aty a time are observed and the model is trained on these events. The model will then be used to predict the fare amount of the next 1000 events. You will compare the performance of the model when trained using the incremental method and the batch method where all training events are observed. 

To clarify the incremental protocol that you will be implementing, in incremental learning you will need to save the model of the previous iteration (each iteration learns from 10000 events and predicts the next 1000) and use it to initialize the model for the next iteration, ensuring that the validation set where the inference happens is not included in any model training dataset. You need to produce 10 iterations. 

To clarify the batch protocol you will be implementing, in batch learning you will need to train the model on 10000 events and compare it to the 10000 events of the incremental model (this comparison must result in the same MSE performance since both are considering 10000 input examples), then train a model with 20000 events and compare to the 2nd iteration of the incremental model and so on. You need to produce the comparison plot of the MSE between batch and incremental model for all 10 iterations.


