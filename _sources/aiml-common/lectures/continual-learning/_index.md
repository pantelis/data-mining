---
title: Continual Learning (CL)
---

# Continual Learning (CL)

## Introduction 

One of the greatest goals of AI is building an artificial continual learning agent which can construct a sophisticated understanding of the external world from its own experience through the adaptive, goal-oriented and incremental development of ever more complex skills and knowledge. 

[![Building Machines that learn and think like humans](https://img.youtube.com/vi/RB78vRUO6X8/0.jpg)](https://www.youtube.com/watch?v=RB78vRUO6X8)

*Building Machines that Learn & Think Like People by Prof. Josh Tenenbaum - Click to watch on youtube*

Continual learning (CL) is essential in many fields such as robotics where high dimensional data streams need to be constantly processed and where naïve continual learning strategies have been shown to suffer from _catastrophic forgetting_ also known as _catastrophic interference_. Take deep learning architectures for example: they excel at a number of classification and regression tasks by using a large dataset, however the whole dataset must be present during the training phase and the  network must be _retrained_ every time there the underlying distribution $p_{data}$ changes.  

The existing approaches of _transfer learning_ (e.g. [here](https://arxiv.org/abs/1901.08149)) that start with weights obtained via a _pretraining_ the network to a suitable existing dataset and fine tune them to complete a similar task in a new dataset are inadequate. They only help on reducing the training time and improve  potentially the  performance for the new task , rather than preserve the pre-existing ability to achieve good performance on the original task. Aside from supervised learning, CL methods accommodate a wider range of tasks such as unsupervised and reinforcement learning.  

Our brains exhibits _plasticity_ that allows us on one hand to integrate new knowledge and on the other hand to do so without overcompensating for new knowledge causing interference with the consolidated knowledge - this tradeoff is called _plasticity-stability dilemma_.  Hebbian plasticity, termed after Hebb's rule (1949), basically postulate the tendency of _strengthening the connection_ between pre-synaptic and post-synaptic neurons when the activations $x$ of the former affect the activations $y$ of the later. 

![pre-post-synaptic-neuron](images/pre-post-synaptic-neuron.png)

In its simplest form, Hebb's rule states that a synaptic strength $w$ changes as: $\Delta w = \eta \times x \times y$ where $\eta$ is the learning rate. Hebb's rule can lead to instability and [homeostatic](https://en.wikipedia.org/wiki/Homeostasis) mechanisms are used, represented by a modulatory feedback control signal $m$ that regulates the unstable dynamics of Hebb's rule:

$$ \Delta w = m \times \eta × x \times y$$

We can draw the block diagram of such dynamical system model:

![Hebbian-Homeostatic-Plasticity](images/Hebbian-Homeostatic-Plasticity.png)
*Hebbian-Homeostatic Plasticity Model for synaptic updates.*

While the synaptic updates under the plasticity rule are essential to avoid catastrophic forgetting at the neural circuit level, we need a system level mechanism to carry out two complementary tasks, also known as Complementary Learning Systems (CLS) theory: 

* _statistical learning_ with the ability to generalize across experiences and retain what it learned for the long term and 
* _episodic learning_ that learns quickly novel information and retains episodic event memories (memorization). 

Statistical learning is implemented by the neocortical functional area of the grain and is a slower process as it extracts statistical structures of perceptive signals to be able to generalize to novel examples / situations. Episodic leanring, implemented in the hypocampus, is much faster as its goal is to learn specific events, retain them and play them back to the neocortex for information integration purposes. Both subsystems use the controlled Hebbian plasticity mechanism outlined earlier. 

![CLS](images/CLS.png)
*Hypocampus and Neocortex complementary learning system*

The aforementioned widely accepted as explanatory functions of the brain learning system, guided computational models and architectures of continuous learning in AI. For the deep learning architectures, three are the main threads: 

![cl-approaches](images/cl-approaches.png)

1. **Regularization** approaches (a), that alleviate catastrophic forgetting by imposing constraints on the update of the neural weights.  
2. **Dynamic architectures** (b/c) that allocate additional neural resources to capture the new knowledge 
3. **CLS-based** approaches. 

## Continual Learning Tutorial

The following video is well received as an introductory treatment on the subject. 

[![Continual Learning and Catastrophic Forgetting](https://img.youtube.com/vi/vjaq03IYgSk/0.jpg)](https://www.youtube.com/watch?v=vjaq03IYgSk)
_Continual Learning and Catastrophic Forgetting Tutorial - click to watch on youtube_

<!-- ## Relationship between Continual and Meta Learning

<div id="presentation-embed-38930881"></div>
<script src='https://slideslive.com/embed_presentation.js'></script>
<script>
    embed = new SlidesLiveEmbed('presentation-embed-38930881', {
        presentationId: '38930881',
        autoPlay: false, // change to true to autoplay the embedded presentation
        verticalEnabled: true
    });
</script> -->
