---
title: Neural Network Assignment
---

# Neural Networks Assignment

## Backpropagation (20 points)

Assuming that $x \in \R^n$, backpropagate the following network to find 

$$\frac{\partial L}{\partial \mathbf w}$$


![](images/neuron-ce.png)

## Tensorflow Playground (60 points. 10 points per question)

The TensorFlow Playground is a handy neural network simulator built by the TensorFlow team. In this exercise, you will train several binary classifiers in just a few clicks, and tweak the model’s architecture and its hyperparameters to gain some intuition on how neural networks work and what their hyperparameters do. 

1. Try training the default neural network by clicking the Run button (top left). Notice how it quickly finds a good solution for the classification task. The neurons in the first hidden layer have learned simple patterns, while the neurons in the second hidden layer have learned to combine the simple patterns of the first hidden layer into more complex patterns. Why that is? 

2. Activation functions. Try replacing the tanh activation function with a ReLU activation function, and train the network again. Does it find the solution faster or slower? Why is that? 

3. The risk of local minima. Modify the network architecture to have just one hidden layer with three neurons. Train it multiple times (to reset the network weights, click the Reset button next to the Play button). Why the training time has a wide variability? 

4. Remove one neuron to keep just two. Notice that the neural network is now incapable of finding a good solution - why that is?

5. Set the number of neurons to eight, and train the network several times. Has the training time (time to convergence) improved? Why that is? 

6. Select the spiral dataset (the bottom-right dataset under “DATA”), and change the network architecture to have four hidden layers with eight neurons each. Notice that training takes much longer and often gets stuck on plateaus for long periods of time. Also notice that the neurons in the highest layers (on the right) tend to evolve faster than the neurons in the lowest layers (on the left). Can you explain how this may be related to gradient flow through the network? 

## Tensorflow API (20 points)

1. (5 points) Submit your notebook URL that allows the notebook [here](https://pantelis.github.io/cs301/docs/common/lectures/cnn/cnn-example-architectures/cnn-classification-workshop/) to be executed. 

2. (15 points) Start reducing the number of cats in the dataset and plot the accuracy of the predicting the cat class as the population of cats becomes 90%, 70%, 50%, 30%, 10% of the original. For each population size present the hyperparameter optimized result using [AutoKeras](https://autokeras.com). Explain your findings. 

