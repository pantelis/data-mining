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

You will need to store the events in an OLAP database that for this assignment will be [DuckDB](https://duckdb.org/docs/installation/index?version=latest&environment=python). You will host DuckDB in the container `app`. Please note that you need to define a volume mapping so your database file is persisted and you dont need to start from scratch if your docker container exited. You will use a local volume mapping for persistence. You will also need to create a table in the database to store the events. The table will have the same fields as the event JSON object.

## Task 4: Data Analysis

