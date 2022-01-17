---
title: Lecture 8 - Markov Decision Processes 
weight: 101
---

# Markov Decision Processes

We started looking at different agent behavior architectures starting from the [planning agents]({{<ref "../planning">}}) where the _model_ of the environment is known and with _no interaction_ with it, the agent improves its policy, using this model as well as problem solving and logical reasoning skills. 

We now look at agents that can plan by:

1. _Interacting_ with the environment still knowing the model (dynamics) of the environment.
2. Receive _reward_ signals after each interaction. 
3. Have an internal _objective_ function that they try to optimize based on the _experience_ they accumulate.

The problem as will see, will be described via a set of four equations called Bellman expectation and Bellman optimality equations that connect the values (utility) with each state or action with the policy. These equations can be solved by Dynamic Programming algorithms to produce the optimal policy (strategy) that the agent must adopt. 

Computationally we will go through approaches that solve the MDP as efficiently as possible - namely, the value and policy iteration algorithms.

![solving-mpd](images/solving-mdp.png)
*Solving MDP Problems*

{{<hint info>}}
Apart from the notes here that are largely based on [David Silver's (Deep Mind) course material](https://www.davidsilver.uk/teaching/) and [video lectures](https://www.youtube.com/watch?v=2pWv7GOvuf0&list=PLqYmG7hTraZDM-OYHWgPebj2MfCFzFObQ), the curious mind will be find additional resources: 

 * [in the Richard Sutton's book](http://incompleteideas.net/book/RLbook2020.pdf) - David Silver's slides and video lectures are based on this book. The code in Python of the book is [here](https://github.com/ShangtongZhang/reinforcement-learning-an-introduction)

* [in the suggested book](https://www.amazon.com/Deep-Reinforcement-Learning-Python-Hands-dp-0135172381/dp/0135172381/ref=mt_paperback?_encoding=UTF8&me=&qid=) written by Google researchers as well as on [OpenAI's website](https://openai.com/resources/). The chapters we covered is 1-4. 

* You may also want to watch Andrew Ng's, [2018 version of his ML class](https://www.youtube.com/playlist?list=PLoROMvodv4rMiGQp3WXShtMGgzqpfVfbU) that includes MDP and RL lectures.

Many of the algorithms presented here like policy and value iteration have been developed in [this](https://github.com/rlcode/reinforcement-learning) git repo that you should download and run while reading the notes. 

{{</hint>}}
