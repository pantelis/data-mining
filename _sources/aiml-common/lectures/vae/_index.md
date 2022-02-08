---
title: Variational Auto Encoders (VAE)
---

# Variational Auto Encoders (VAE)

We have seen in the treatment of CNNs that they can generate features that are suitable for the classification or regression task at hand using the labels to guide the maximization of the log-likelihod function. Here we are looking at the problem where we need features that are suitable for generating data from the input distribution without necessarily having labels. 

In this setting we will look deeper into a major family of variational inference: the VAE. Variational Autoencoders (VAEs)[^3] are popular generative models being used in many different domains, including collaborative filtering, image compression, reinforcement learning, and generation of music and sketches. 

[^3]: Here we treat the continuous VAEs. 


## References

[1]: Diederik Kingma and Max Welling. Auto-Encoding Variational Bayes. In _International Conference on Learning Representations_, 2014, https://arxiv.org/abs/1312.6114

[2]: Yuri Burda, Roger Grosse, Ruslan Salakhutdinov. Importance Weighted Autoencoders. In _International Conference on Learning Representations_, 2015, https://arxiv.org/abs/1509.00519
    