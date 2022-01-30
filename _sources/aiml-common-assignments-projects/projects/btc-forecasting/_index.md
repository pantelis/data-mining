---
title: BTC Deep Forecasting
---

# BTC Deep Forecasting

![](images/btc.gif)

In this project we will be forecasting the price of an asset or commodity. To exponentially increase your cool factor within your social network, you are tasked to predict the daily (trading days only) closing price in USD of Bitcoin (BTC). 

---
DISCLAIMER

THIS IS A CLASS PROJECT POSTED FOR EDUCATIONAL PURPOSES ONLY. IF YOU FOLLOW THE METHODS AND PREDICTIONS POSTED BY STUDENTS, YOU ARE ALMOST CERTAINLY GUARANTEED TO LOOSE ALL YOUR CRYPTO OR REAL MONEY. THE REASON IS SIMPLE: ALTHOUGH WE DO NOT CONSTRAINT THE PREDICTOR VARIABLES OR THE APPROACHES, MOST OF THE STUDENTS WILL IMPLEMENT A FORECASTING METHOD BASED ON HISTORICAL BTC DATA. SINCE **ALL** FUTURE PRICES MOVE AS A RESULT OF THOUSANDS OF OTHER FACTORS (DATA) OTHER THAN HISTORICAL PRICES, YOU WILL SUFFER THE INEVITABLE SHOULD YOU BE FOOL ENOUGH TO BET ON SUCH PREDICTIONS. THE AUTHOR OF THIS PROJECT DESCRIPTION BEARS NO RESPONSIBILITY FOR YOUR IRRESPONSIBLE TRADING ACTIONS.

---


## Environment set up (0 points)

You will use google Colab for authoring your forecaster. You are also welcomed to set up an AWS account and use the [AWS Forecast](https://docs.aws.amazon.com/forecast/latest/dg/what-is-forecast.html) service. No matter what you do however we can provide limited support for IT issues in your environment. 


## Data (10 points)

In this project you don't need to think about Kafka and other pub/sub or message broker technologies that ingest data in production systems. You may retrieve and store all historical data you want to use (there is no time limit on the past) but you will implement a system that can update its models as "new" data are coming in. 

So lets assume you define as a _window_ data between `collection_start_date` and `collection_end_date`. You are free to collect as many windows of data as you wish and you are also free to determine the best window size.  The only constraint is that predictions you will report results on must be all trading days between Nov 1st 2021 and Dec 1st 2021 without repetition (aka. without predicting twice the same date).  

<!-- You will be predicting the BTC-USD price for **each of the last T=7 calendar days** of your window.  

![](images/forecasting.drawio.png) -->

## Tweet Sentiment Analysis (30 points)

Use the Twitter API and Python libraries that can access it to bring tweets you consider as relevant to the price prediction. 

1. You need to implement a tweet feed filter that will an encoder that will embed each tweet in a vector space and allow you to determine its sentiment (15 points)
2. You are also responsible for figuring out how to transform (eg average) the sentiments themselves so that they can be used by the price predictor (15 points)   



## Price Predictor Development (50 points)

Follow [these](https://www.analyticsvidhya.com/blog/2021/06/download-financial-dataset-using-yahoo-finance-in-python-a-complete-guide/) instructions to bring the BTC-USD price data required in this project. 

### DeepAR (15 points)

In [this paper](https://arxiv.org/pdf/1704.04110.pdf) a methodology for producing accurate probabilistic forecasts, based on
training an auto-regressive recurrent network model is shown. RNNs will be covered in our lectures so there is no need to panic. 

You will implement [in TF](https://github.com/arrigonialberto86/deepar) or PyTorch the method and present your predictions. 


### Facebook Prophet (15 points)

You need to understand the principles behind the [Prophet prediction method](https://facebook.github.io/prophet/) and implement it for the problem at hand. 

### Predictor Documentation (20 points)

You will write a 2-page single spaced summary (excludes figures) in markdown on how _each_ predictor works (4 pages total min). You need to refer to corresponding code sections as you describe the functions. 


## Results (10 points)

1. Post a table with your prediction vs actual price as well as include a plot of the two time series over time.  
2. Provide any intuition around the forecasting method you adopted. 

Our advice is to create a skeleton of the project first with all parts involved without spending a lot of time on algorithm finetuning. Finetune after you have your draft predictions first.