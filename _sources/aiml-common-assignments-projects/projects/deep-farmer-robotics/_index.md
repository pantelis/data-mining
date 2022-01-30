---
title: Deep Farmer Robotics
---

# Deep Farmer Robotics

In a world that that is quickly changing from the evolving weather to new requirements or demands for truly  organic products with no chemicals, there is a need to innovate quickly in the field of weeding - one of the most important and expensive activities farmers face today. 

{{<youtube "ZdcgvreJLqk">}}

In this project you will develop a robotic AI agent in AWS Robomaker that kills individual weeds with laser.  The agent must be developed in AWS Robomaker for the ROS2 Foxy distribution.  

## Weed perception system

The perception system of the agent includes a weed detection pipeline powered by [this dataset](https://www.nature.com/articles/s41598-018-38343-3) You will use a pipeline similar to [this](https://medium.com/pytorch/ai-for-ag-production-machine-learning-for-agriculture-e8cfdb9849a1). Your task is to replicate the results presented in terms of performance (eg. F1 score) and author a report explaining the implementation and the challenges you met. 

## Navigation perception system

TBD

## ROS2 Robot Model

You will need to construct the robot model such as this one. 

## Gazebo environment model

You need to construct the model of the field that the robot will be used on. Generative modeling can be used to create weeds and plants. 

## Planner

TBD

<!-- 
Read [this](https://arxiv.org/pdf/2003.03726.pdf) paper and watch the following video that describes a method where a PDDL planner can be "fed" from a dynamically changing environment. 

{{<youtube Zzi29kSKlcE>}}

You will use [Navigation 2](https://navigation.ros.org/) stack to integrate with the root controls  -->
