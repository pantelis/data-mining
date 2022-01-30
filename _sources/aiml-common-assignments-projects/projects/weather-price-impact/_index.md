---
title: Weather Impact on NYC Taxi Fare
---

#  Weather Impact on NYC Taxi Fare

This project is a continuation in part of the [NYC taxi fare prediction] and asks a simple but not so straightforward to answer question:

> Everything else being equal (ceteris-paribus)  how much additional far should people expect to pay when the weather is bad?

Some of the reasons why this question may be challenging , although there are notebooks in Kaggle that try to address it,  are:

1. The dataset needs augmentation with weather data (people have done this in Kaggle and you can too)
2. When the weather is bad, the demand shifts both temporally and spatially. 
3. When the weather is bad the trip durations are longer due to either weather _or_ congestion. 

You need to provide your answer as a table of 100 dominant zones (pickup - dropoffs) with the predicted % fare _difference_ across all types of bad weather (rain, snow etc.)

A zone is a geographic (lat, long) area of [100m x 100m]. It is dominant if the pickups or dropoffs are much higher compared to another.

