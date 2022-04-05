# Fashion MNIST From Scratch Assignment

There are plenty of examples that train a neural network scratch example  [this handwritten digit recognition MNIST example](https://github.com/joelgrus/data-science-from-scratch/blob/master/scratch/deep_learning.py). 

## Step 1: Fashion MNIST Dataset (10 points)

Download the fashion MNIST dataset and convert it to a dataset that is suitable for binary classification.

## Step 2: Architecture (20 points)

Dimension a network that consist of a dense (fully connected) ReLU layer and a sigmoidal layer that will satisfy the task (binary classification). 

## Step 3:  Backpropagation (30 points)

![](images/backprop-simple-dnn.jpg)

Understand and write in your notebook using latex math syntax the backprop equations. (10 points)

Use these equations to write the backprop function and train the network using the SGD algorithm. (20 points)


## Step 4: Momentum (40 points)

(20 points) Describe clearly the differences between SGD and the Momentum algorithm and obtain the precision vs recall curve for the network above for values of hyperparameters you have chosen. 

(20 points) Use hyperparameter optimization to tune the hyper parameters of each algorithm and obtain the final precision vs recall curves for both. Its up to you to choose the hyperparameter method and library - this can be as simple as GridSearch but this of course will impact your results.  

Any notebook or py code + markdown submission that lacks explanations will receive minimal points. 