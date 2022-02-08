---
title: Natural Language Processing
---

# Natural Language Processing

![national-library-greece](images/national-library-greece.jpg)
*“You shall know a word by the company it keeps” (J. R. Firth 1957: 11) - many modern discoveries are in fact rediscoveries from other works sometimes decades old. NLP is non an exception.*

In this chapter we will start discovering how agents can process _and respond_ to input sources that contain natural language. Such inputs are all the the trillions of web pages, billions of captioned videos, real-time multi-modal speech and video etc.  We wil rewind developments in this space starting in 2012 to discover how J.R. Firth's words translate to the NLP space as it evolved over the last 8 years.

We start though by augmenting the overall agent architecture with blocks that bring the language domain in the picture as shown below:

![overall-agent-architecture](images/overall-agent-architecture.png)
*Overall AI agent architecture and language components*

After going over the next few sections the rationale behind the assignment of these blocks in the corresponding subsystems of the agent will be made apparent to you. To start with explaining the approach we will follow here, similar to what took place in the ML field in general, classical methods in NLP are largely superseded by deep learning architectures. Our focus will be towards the later deep architectures and the changes that took place after 2012. On the other hand we need to cover certain stages that are common to both approaches - these stages are processing the text to allow representation learning stages to be able to function.  

Most of the material presented here are from the sources below:
> * [CS224n: Natural Language Processing with Deep Learning](http://web.stanford.edu/class/cs224n/) - see also the [2019 version of the video lectures](https://www.youtube.com/playlist?list=PLoROMvodv4rOhcuXMZkNm7j3fVwBBY42z)
> * [Natural Language Processing in Action](https://www.amazon.com/Natural-Language-Processing-Action-Understanding/dp/1617294632). This book takes a hands on perspective to NLP. It uses both nltk (originally targeting students and researchers) and spacy (originally targeting development for production) for implementing some of the stages of the NLP pipelines.
