---
title: Logical Agents
draft: false
---

# Logical Agents

In this chapter we see how agents equipped with the ability to represent internally the state of the environment and reason about the effectiveness of possible actions using propositional logic, can construct plans that are guaranteed to achieve their goals. We start with the KB we developed in wumpus world and enhance it by introducing representations that avoid looking back at the whole percept history to make an inference about the state of the environment currently. 

## Enhancing the KB

We add a couple of sentences in the KB we had developed,focusing on axioms (facts or rules that evaluate to TRUE). When these axioms involve variables that they never change we call such variables _atemporal_. This is shown in the next table.

| Sentence | Description | KB |
| --- | --- | --- | 
| $R_1$ | There is no pit in cel [1,1] | $\neg P_{1,1}$ |
| $R_2$ | The cell [1,1] is breezy if and only if there is a pit in the neighboring cell. | $B_{1,1} ⇔ (P_{1,2} \lor P_{2,1})$ | 
| $R_3$ | The cell [2,1] is breezy if and only if there is a pit in the neighboring cell. | $B_{2,1} ⇔ (P_{1,1} \lor P_{2,2} \lor P_{3,1})$ |
| $R_4$ | The cell [1,1] is stenchy if and only if there is a wumpus in the neighboring cell. | $S_{1,1} ⇔ (W_{1,2} \lor W_{2,1})$ | 
| $R_5$ | There is only one wumpus in this world. | | 
| $R_{5-1}$ | There is at least one wumpus | $W_{1,1} \lor W_{1,2} \lor ... \lor W_{4,4}$  |
| $R_{5-2}$ | There is at most one wumpus | | 
| $R_{5-2-1}$ | | $\neg W_{1,1} \lor \neg W_{1,2}$ | 
| $R_{5-2-2}$ |  | $\neg W_{1,1} \lor \neg W_{1,3}$ | 
| ... |  | ... | 
| $R_{5-2-N}$|  | $\neg W_{4,3} \lor \neg W_{4,4}$ |


With respect to percepts and and in fact with everything in the world that is dynamic, we introduce the notion of _time_ ($t$) and index all such variables accordingly. We do so to avoid the situation where we have conflicts in the KB where while in cell [1,2] we store in the KB $\mathtt{Stench}$ and in another instance e.g. in cell [2,2] we store $\neg \mathtt{Stench}$. These type of variables are called some times called _fluent_ but effectively these are the usual mutable state variables. Location as we have seen is a primary variable that is carried by the environment state. We can then define an associated fluent $L_{x,y}^t$ and store the following sentences in the KB. 

| Sentence | Description | KB |
| --- | --- | --- | 
| $R_6$ | if an agent is in cell [x,y] at $t$ and perceives [Stench, Breeze, Glitter, Bump, Scream]=[None, Breeze, None, None, None] then the cell is a Breeze cell | $L_{x,y}^t \implies (\mathtt{Breeze}^t ⇔ B_{x,y})$ | 
| $R_7$ | if an agent is in cell [x,y] at $t$ and perceives [Stench, Breeze, Glitter, Bump, Scream]=[Stench, None, None, None, None] then the cell is a Stench cell | $L_{x,y}^t \implies (\mathtt{Stench}^t ⇔ S_{x,y})$ | 

Similar to percepts, actions also are taken at specific times $t$. By convention, we first receive a percept at $t$, then take an action during the same time step $t$ and then the environment transitions to another state at $t+1$. To specify the transition model that describes how the world changes we use _effect axioms_ as follows:

| Sentence | Description | KB |
| --- | --- | --- | 
| $R_8$ | if an agent is in cell [1,1] at $t=0$ and is $\mathtt{FacingEast}$ and decides to move $\mathtt{Forward}$ it will transition to $L_{2,1}$ in the next time step | $L_{1,1}^0 \land \mathtt{FacingEast}^0 \land \mathtt{Forward}^0 \implies (L_{2,1}^1 \land \neg L{1,1}^1)$ | 

There lies a serious issue. There is a combinatorial explosion problem as we have to repeat sentences like the $R_8$ for each of the possible $T$ time steps into the future that include actions. For a single $\mathtt{Forward}$ action we need to consider $4 x T x n^2$ possibilities, where 4 are the possible agent orientations and $n^2$ is the number cells in the wumpus world! But there are more bad news. We need to also include in the KB was remains _unchanged_ - this is a well known issue called the **representation frame problem**. It took its name from the video frame where most of the pixels stay unchanged (background) and only a few change (foreground). Imagine the bandwidth that we need to consume to transmit _all_ video frame pixels.  This is analogous to the KB - imagine the combinatorial explosion if we have to specify sentences for everything that stays the same at every time instant. As an example we will have to specify that the wumpus is alive at $t+1$ as it was at $t$, that the agent continues to have one arrow when it didn't use it and a myriad other intuitively obvious axioms. 
