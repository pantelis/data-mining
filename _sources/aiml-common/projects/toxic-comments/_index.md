---
title: Toxic Comment Classification
---

# Toxic Comment Classification

![toxic-comment](images/toxic-comment.jpg)


The internet has been converted from a tool offering unprecedented utility to mankind to a tool that can can destabilize societies and ven cause individuals to take their own lives [cite](https://www.nytimes.com/2018/08/08/technology/personaltech/internet-trolls-comments.html). 

Discussing things you care about can be difficult. The threat of abuse and harassment online means that many people stop expressing themselves and give up on seeking different opinions. Platforms struggle to effectively facilitate conversations, leading many communities to limit or completely shut down user comments.

The Conversation AI team, a research initiative founded by Jigsaw and Google (both a part of Alphabet) are working on tools to help improve online conversation. One area of focus is the study of negative online behaviors, like toxic comments (i.e. comments that are rude, disrespectful or otherwise likely to make someone leave a discussion). So far they’ve built a range of publicly available models served through the Perspective API, including toxicity. But the current models still make errors, and they don’t allow users to select which types of toxicity they’re interested in finding (e.g. some platforms may be fine with profanity, but not with other types of toxic content).

In [this competition](https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge), you’re challenged to build a multi-headed model that’s capable of detecting different types of of toxicity like threats, obscenity, insults, and identity-based hate better than Perspective’s current models. You’ll be using a dataset of comments from Wikipedia’s talk page edits. Improvements to the current model will hopefully help online discussion become more productive and respectful.

