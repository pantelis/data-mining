---
title: Backprop Workshop in Tensorflow
---

# Backprop Workshop in Tensorflow

## Tensorflow Autodiff (Eager Mode)

TensorFlow's eager execution is an imperative programming environment that evaluates operations immediately, without building graphs. We are usually using the computational graph in production environments. So eager is the way to do TF since operations return concrete values instead of constructing a computational graph to run later. This makes it easy to get started with TensorFlow and debug models, and it reduces boilerplate as well. To follow along with this guide, run the code samples below in an interactive python interpreter. 

To be able to follow the notebook you need to make sure you have reviewed first the following notebooks. 

* [Eager Mode](https://www.tensorflow.org/guide/eager)
* [Tensors](https://www.tensorflow.org/guide/tensor)
* [Variables](https://www.tensorflow.org/guide/variable)

{{<hint warning>}}
**How to Run**: Click the yellow button found under the title "Run in Google Colab". 
{{</hint>}}

<iframe src="https://nbviewer.jupyter.org/github/tensorflow/docs/blob/master/site/en/guide/autodiff.ipynb" width="900" height="1200"></iframe>

## TF Graphs

<iframe src="https://nbviewer.jupyter.org/github/tensorflow/docs/blob/master/site/en/guide/intro_to_graphs.ipynb" width="900" height="1200"></iframe>