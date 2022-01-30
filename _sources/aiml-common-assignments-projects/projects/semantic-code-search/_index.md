---
title: Semantic Code Search
---

# Semantic Code Search

**This project is due May 10 at 11:59pm**

Imagine a world where software is automatically generated and stitched together to create complex distributed / reactive systems that can solve the problem at hand. In this course you got to appreciate the systems approach to AI and this project will allow you to understand one very important facet of automatic AI system synthesis: a search engine for code. It can be used initially by human programmers and later by robots to find pieces of code that are relevant to the target function. 

Semantic code search is the task of retrieving _relevant code_ given a _natural language_ query. While related to other information retrieval
tasks, it requires bridging the gap between the language used in code (often abbreviated and highly technical) and natural language
more suitable to describe vague concepts and ideas.

In this project you will use the [CodeSearchNet Corpus](https://arxiv.org/pdf/1909.09436.pdf) and participate in the corresponding [challenge.](https://github.blog/2019-09-26-introducing-the-codesearchnet-challenge/). In this project you will focus **only** on Python language and the associated  dataset contains about 0.5 million pairs of function-documentation pairs and about another 1.1 million functions without an associated documentation. You are required to submit your Normalized Discounted Cumulative Gain (NDCG) score for **only** the human annotated examples. 

Steps to complete this project:

1. Follow the [setup instructions](https://app.wandb.ai/github/codesearchnet/benchmark).
   
2. Implement and explain a [baseline model](https://github.com/github/CodeSearchNet) e.g Self-Attention and try to improve its performance over the Elastic Search baseline. You are free to try to develop your own model.

3. Follow the instructions in the competition to submit your score to the leaderboard and submit your github / colab notebooks and writeups.  

Despite the fact that the project is not mandating the invention of new methods, the project is challenging - teams each with a maximum of three students are allowed.