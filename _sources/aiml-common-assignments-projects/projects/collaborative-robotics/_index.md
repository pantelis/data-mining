---
title: Collaborative Robotics
---

# Collaborative Robotics

You are a co-founder in a startup called PodGrocer, a company that deploys pods to selected host sites such as electric vehicle charging stations, mall parking lots and can also attach to existing supermarket stores. Each pod was constructed by modifying a standard shipping container and is cooled by latest technology green energy backed up by the host site power feeds. 

{{<hint info>}}
The shipping container sized pod is irrelevant for this project but its provided here as they are routinely used as building blocks for larger and sometimes movable structures. 
{{</hint>}}

The system in operation is shown in the following video

{{<youtube n5G3KfE8PVc>}}

How the company generates revenue: 

1. Customers order via PodGrocer's or partners web site. Partner's fulfillment center places the order in a standard container called a tote (blue container). Multiple totes populate a palette that can be moved around by a mobile robot. 

2. The pod is replenished by a truck delivery driver (or fulfillment center personnel if the pod is attached to an existing facility). They roll the palette in via the pod's loading bay and from that point onwards, everything is automated. 

3. Customers that orders groceries and other goods, pick up their order via an ATM-like hutch.  The customer's app provides an estimate as to when the customer is expected to be at the pod location. After arrival and authentication, the system is able to deliver the relevant to the order totes to the customer at the pick up hatch in seconds. 

See [this video](https://www.youtube.com/watch?v=IqYk0dFcZgc&t=2s) for more details of the robotic pod operations. 

## Tasks

In this project you will perform certain tasks to ensure that the pod is able to perform its required robotic functionality and function as a system. The implementation must be resilient and therefore the system must be distributed across many nodes supported by the ROS as well as use a number of AWS managed services. Usage of AWS managed services are not required for this project.  

The Robot Operating System (ROS) is a set of software libraries and tools for building robot applications. From drivers to state-of-the-art algorithms, and with powerful developer tools, ROS has what you need for your next robotics project. And it’s all open source. [Here](https://docs.ros.org/en/foxy/index.html) you will find the official documentation on ROS 2, the newest version of ROS that you will use.
 
 The functionality is divided into subsystems such as the planner responsible for computing a path to the goal state and other navigation control subsystems such as recovery and localization. 

The task you need to do is to implement and use the above subsystems to coordinate the transfer of pallets inside a pod. For all tasks below please consult the [wiki pages](https://github.com/pantelis-robotics/aws-warehouse/wiki) as well. Students that have significant contributions to the wiki way will be considered for extra credit points.  For example, students can add Win10, mac and AWS robomaker platform details. 

### Task 1 (10 points) 

Execute the docker installation scripts in [this gude](http://jderobot.github.io/RoboticsAcademy/exercises/MobileRobots/multi_robot_amazon_warehouse/) and bring up the environment. See the wiki for details. 

### Task 2 (30 points)

Write the planner in python under src/exercise.  The following are the planner requirements: 

1. The robots must start from known locations for each delivery. Fix the location using the 2D Pose Estimate in RViz. 

2. No robots should collide with each other and they should not wonder without purpose in the environment. 

3. Both robots must be active at the same time and carry palettes to selected destinations (goal states). 
   
The planner can be triggered interactively i.e. it can only start when a mouse is clicked in RViz. Each robot must move at least 2 pallets to storage location (south of the room) with the first attempt. 

### Task 3 (30 points)

Use the symbolic planning language PDDL to write a planning controller that integrates Plansys2 and Nav2.  See the Dock-Worker Robots Planning Domain [in this post](https://towardsdatascience.com/improving-classical-ai-planning-complexity-with-planning-graph-c63d47f87018) as well as the [PlanSys2 tutorials](https://intelligentroboticslab.gsyc.urjc.es/ros2_planning_system.github.io/tutorials/docs/bt_actions.html). 

The controller is may be triggered by an event i.e. customer arriving in the pickup hatch location. 

### Task 4 (30 points)

Write a markdown report where you explain your design of the planner in Task 2 and 3 as well as providing positive and negative results from the robotic delivery of the pallets. Explain the negative results and suggest ways that can be fixed if you have no time fixing these issues. 

#### Notes: 

{{<hint alert>}}
To help plan the tasks amongst the team members please use Trello (login with your nyu account). Submit your Trello boards with your project.  

Note that the points are assigned per task completion and are relatively independent on the implementation complexity. Therefore start simple and make sure you submit all completed tasks rather than spending time on the ultimate path planner and miss the deadline.  
{{</hint>}}


{{<hint warning "WARNING">}}

Consider using AWS Robomaker for this project (ROS2 distribution). 

Note to all students using AWS resources provided for this project. You are **entirely** responsible to limit the use of p2.xlarge instances that consumes on-demand 1$/h and use CPU instances when possible. Invest in understanding docker containers so you do not suffer catastrophic failures when working in a cloud environment (the norm in practice).  You are responsible for not exceeding your budget.

{{</hint>}}