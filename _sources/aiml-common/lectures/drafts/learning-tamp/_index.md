---
title: Learning-based Task and Motion Planning
---

https://discourse.ros.org/t/ros2-planning-system-1st-anniversary/18224/6

Multiple people here seem to be interested in Task and Motion Planning (TAMP/TMP).

It’s a relatively big research field with many approaches/contributions.

As a recent example, RSS20 featured an interesting workshop 2 on TAMP & Learning. As you can see from the talks it’s a rather open field people are actively looking into.

Traditionally, the symbolic reasoning side often views TAMP as a particularly difficult instance of SMT Planning, and the motion planning side might argue it’s a motion planning problem with an unknown plan skeleton. Both perspectives have their merits.

My biggest question marks are A) how to convert a real world scene to a PDDL problem in a useful way, B) make sure the symbolic plan is executable (this is not trivial for any manipulation task) and C) what to do when a step turns out to be infeasible or fails.

A:
Traditionally, this is hand-crafted since Shakey’s time 1.
With the advent of complex knowledge graphs/ontologies, researchers looked more into generating planning descriptions (or even just inferring goal conditions for a known domain) on the basis of ontologies. The KnowRob system 1, developed under Michael Beetz, is a prime example of this approach. It still remains a hard problem to keep the domains consistent and provide enough information to produce the desired outcomes. That being said, with a lot of engineering effort it can produce impressive results.

A quite neat combination that generates planning domain facts from perceived scenes can be found in Chris Paxton’s research (they also gave a talk at the workshop I linked). They employ learning-based systems to generate domain facts from camera input.

B:
If you look into SMT problem solvers, they discriminate between eager and lazy solvers.

The latter approach is quite straightforward: you find a symbolic plan that’s valid according to your planning domain and then attempt to solve the resulting problem with a dedicated solver (in this case a motion planner). MP solvers are notoriously anytime algorithms, so you either end up with an incomplete TAMP solver or a complex anytime system.

Eager approaches try to encode everything relevant about the problem in the planner itself.

Some people try this with TAMP by encoding predicates like reachability directly. In practice though, they either have to come up with geometric heuristics for it, or they have to solve the MP problem to reach the object under the hood. Viewing the problem from the motion planning side, “making sure the plan is executable” is not a problem at all because they only consider executable trajectories. But they fight with many more local minima that way.
A noteworthy example that comes from the motion-planning side, but combines it with logic inference is Logic-Geometric Programming 2 introduced by Marc Toussaint.

C:
That’s recovery behavior and approaches differ (of course they do).
For repeatable actions, you can try again. But how often should you retry before giving up trying to push the damn button?
The obvious choice is plain replanning. In practice you might end up with long delays and oscillating behavior though.
Some projects introduced repair techniques that, e.g., attempt to instantiate an assumed object that’s not found with a different object that might be around (“just use a different glass then”).

Also, have you considered symbolic planning like this in the context of MoveIt Task Constructor?

If you read the introduction to our ICRA19 paper you see that MTC aims for a middle ground.
The goal of the framework is not to solve general TAMP problems, but to provide a systematic structure for tasks more general than A-to-B Motion Planning, but easier than “I want to drink something”. The main reason for this ambition is that general TAMP solvers can generate unexpected robot behavior. That might be exactly what you want it to do to show adaptive behavior, but it might also break your beautiful workflow & demo if the system suddenly decides to use a different tool. Tuning TAMP solvers to generate only solutions you actually consider valid is quite hair-raising at times.

That being said, MTC could theoretically be used as a lazy domain solver in an SMT setting, but it would be a lot of work.

Hope that answers your seemingly simple question :slight_smile:
