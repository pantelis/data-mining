---
title: Planning with Search 
---

# Planning with Search 

In [logical agents]({{<ref "../../logical-reasoning/logical-agents">}}) we have seen that symbolic representations enriched with propositional logic in the Knowledge Base allow us to reason and come up with a sequence of actions that the agent needs to execute to reach the goal. This section provides the background that _connects_ the domain-independent planner that solves the planning problem to _search_. To do so, it is instructive to look initially to problems that are simpler in terms of state and action representation. We effectively zoom out from the  _factored_ representation of the environment's state and treat it as _atomic_ i.e. not broken down into its individual variables. 

Atomic state representations of an environment are adequate for a a variety of global planning tasks:  one striking use case is path planning There, the scene or environment takes the form of a global map and the goal is to move the embodied agent from a starting state to a goal state. If we assume that the global map takes the form of a grid with a suitable resolution, each grid tile (or cell) represents a different atomic state than any other cell. Similar considerations can be made for other forms of the map e.g. a graph form. 

Given such state representation, we will use _search_ to find the action sequence that the agent must produce to reach a goal state. Note that in most cases, we are dealing with _informed_ rather than _blind_ search, where we are also given task-specific knowledge (that we use to develop suitable heuristics) to find the solution as we will see shortly. 

## Maps

We will develop the algorithm for the task at hand which is to find the path between a starting state and the goal state in a map. Not just any path but the _minimum cost_ path when the state transition graph is revealed incrementally through a series of actions and associated individual costs (cost function). The task is depicted below. 

![path-finding](images/parking-lot.png)
*A map of a parking lot as determined via postprocessing LIDAR returns. Obstacles colored in yellow are tall obstacles, brown obstacles are curbs, and green obstacles are tree branches that are of no relevance to ground navigation.*

In practice, maps likes the one above are local both in terms of space (each snapshot is relative to the location of the agent) as well as in terms of time (at the time the agent took these measurements). We can take any map like the one above and form its discrete equivalent such as shown below. We usually call this type _metric map_ and for the purposes of this chapter this is our search area and in it lie all possible feasible _solutions_, each is a _sequence of actions_ distinguished by _path cost_. In this example, the least cost path is actually the geographically longer path - the line thickness for each of the two possible solutions in this figure is proportional to its cost. 

![cost-definition](images/cost-definition.png)
*An example search area with action-cost function where left turns are penalized compared to right.This is common penalization in path planning for delivery vehicles.*

The alternative map representation is _topological_ where the environment is represented as a graph where nodes indicated significant grounded features and edges denote topological relationships (position, orientation, proximity etc.). The sometimes confusing part is that irrespectively of metric or topological representations, the _forward search_ methods we look in this chapter all function on _graphs_. 


##  Search Algorithms Interactive Demo 

This [demo](https://qiao.github.io/PathFinding.js/visual/) is instructive of the various search algorithms we will cover here. You can introduce using your mouse obstacles in the canvas and see how the various search methods behave. 

<iframe src="https://qiao.github.io/PathFinding.js/visual/" width="900" height="1200"></iframe>


{{< hint info >}}
Although the treatment above is self-contained, if you are missing some algorithmic background, afraid not. There is a free and [excellent book](http://algorithmics.lsi.upc.edu/docs/Dasgupta-Papadimitriou-Vazirani.pdf) to help you with the background behind this chapter. In that book Chapters 3 and 4 are the relevant ones.

{{< /hint >}}