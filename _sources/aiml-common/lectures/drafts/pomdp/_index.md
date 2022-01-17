---
title: Partially Observed MDP
weight: 103 
draft: true
---

# Partially Observed MDP 

In [the MDP chapter]({{<ref "../../mdp/mdp-intro">}}) knows the environment state $S^e_t$. In this chapter the agent uses perception and probabilistic reasoning subsystems to internally estimate the environment state $S^i_t$ using the probabilistic graphical models behind [recursive state estimation]({{<ref "../../pgm">}}) where a _belief_ regarding the environment state was formulated or [RNN models]({{<ref "../../rnn">}}).  This distinction between environment state $S^e$ and what the agent estimates, is the difference between fully observed ($S^i = S^e$) and partially observed ($S^i ≠ S_e$) environments we treat in this chapter.

## The POMDP Agent-Environment Interface

The following table summarizes the notation behind the POMDP defined as the tuple $\mathcal M = <\mathcal S, \mathcal P, \mathcal Z, \mathcal R, \mathcal A, \gamma>$

| Symbol  | Description  |
|:-:|---|
| $A_t$ | agent action within time step $t$, $a \in \mathcal{A}$ the finite set of actions |
| $S_t$ | environment state within time step $t$, $s \in \mathcal{S}$ the finite set of states|
| $Z_t$ | observation or measurement that is governed by model $\mathcal Z$ also known as observation function | 
| $R_{t+1}$ | reward sent by the environment after taking action $A_t$ |
| $t$ | time step index associated with each tuple ($S_t, A_t, R_{t+1}$) called the *experience*. | 
| $T$ | maximum time step beyond which the interaction terminates |
| _episode_ | the time horizon from $t=0$ to $T$ |
| $\tau$ | _trajectory_ - the sequence of experiences over an episode |
| $G_t$ | _return_ - the total discounted rewards from time step $t$ - it will be qualified shortly. |
| $\gamma$ | the discount factor $\gamma \in [0,1]$ |

Relative to MDP, the  only new row added is the observation / measurement row since now we use the perceptions to estimate the state. The measurement model is given by

$$Z_{s^\prime, z}^a = p(Z_{t+1}=z | S_{t+1}=s^\prime, A_t = a)$$

The episodes that we observe are 



