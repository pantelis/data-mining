---
title:  Data Science 360
weight: 3
draft: false
---

# Data Science 360

_What are the disciplines that we need to cross fertilize to get a system that possesses intelligence?_

Lets start with a diagram that show not only the disciplines but also _a way of working_ for the many specialists involved.

![axes-ml-development](images/axes-ml-development.svg)

The diagram above highlights three fundamental axes that can deliver a system-based approach to AI. The Z axis is the scientific axis where many disciplines such as psychology, neuroscience, mathematics and others make progress on. The X axis involves the ML/AI communities that borrow ideas from their colleagues in sciences and convert those theories and pragmatic findings into abstractions (models and methods). The model of the neuron, the perceptron, appeared in psychology journals many decades ago and despite its simplicity it is still the unit via which much more complicated neural networks are constructed from.  Todays' models of Long-Term Short-Term Memory (LSTM), Replay Memory and many others not shown in the diagram (as its currently in draft form) are abstractions (models) of discoveries that scientists produced after tens of years of research.  To *use* however these methods and models effectively, major hardware and software components need to be developed also known as computational _frameworks and platforms_ - these live in the Y axis.  Tensorflow and PyTorch are good examples of such frameworks on the software side. They are very important for the development of AI field that is known to be heavily experimental, requiring especially at the perceptive frontend significant computational power and automation. On the hardware side, we have seen tremendous computing advances by [NVIDIA](https://developer.nvidia.com/cuda-zone), [AMD](https://www.amd.com/en/graphics/servers-radeon-instinct-deep-learning) and recently [Intel](https://www.intel.com/content/www/us/en/artificial-intelligence/overview.html) in developing acceleration platforms that allow the software frameworks to satisfy the application latency/throughput requirements. 

At a very high level, progress is made via the counterclockwise iteration $Z  \rightarrow X  \rightarrow Y  \rightarrow Z $. 

Engineers look at the neuroscience/psychology axis,  map discoveries to points in the methods / models axis, and finally develop these methods in hardware architectures and software frameworks. But what can explain the Y -> Z flow? Frameworks in turn help the neuroscientists and psychologists as they can provide generative models of their own discoveries or help them simulate conditions that are not possible using their native tools. 

This counter-clockwise circular multidisciplinary iteration acts as a positive feedback loop accelerating the progress in the AI space.

In this course we will be focusing on the *methods/models* and *frameworks* axis and understand what these models can offer us and how we can apply them in synthesizing an system that can possess intelligence at least for a domain of interest. 
