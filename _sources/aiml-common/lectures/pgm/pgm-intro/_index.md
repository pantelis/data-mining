---
title: Introduction to Probabilistic Reasoning
weight: 81
draft: false
---

# Introduction to Probabilistic Reasoning

In the [scene understanding]({{<ref "../../scene-understanding/scene-understanding-intro">}}) chapter we started putting together the perception pipelines that resulted in us knowing where are the objects of interest in the image coordinate frame but we stopped short of any advanced methods that can lead to what we humans call _understanding_. We hinted that assigning an object an symbolic identity is an essential ability that allows an embodied AI agent to reason about the scene using symbolic reasoning approaches researched by the AI community over many decades. 

![prob-reasoning-agent](images/prob-reasoning-agent.png)
*Positioning of probabilistic reasoning subsystem*

Staying in this trajectory, we introduce the topic of reasoning via a probabilistic lens. We argue that enhancing the environment state as determined by the perception subsystem, includes another subsystem that we will call _probabilistic reasoning_ subsystem that allow us to:

* infer the hidden state of the environment _and_ 
* learn the state that the agents internally maintains via appropriate to the task _representations_. 
  
In a subsequent chapter we will enhance the model to include past _actions_ rather than just past percepts. Let us now start with the rule that is the cornerstone of probabilistic modeling and reasoning - the Bayes rule. 

