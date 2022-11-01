# Mask R-CNN Semantic Segmentation

The semantic segmentation approach described in this section is [Mask R-CNN based on this paper](https://arxiv.org/abs/1703.06870) paper. 

In the object detection section we saw R-CNN that simply cropped proposals, generated externally to the detector, from the input image and classifies  those proposals. Since the proposals were typically overlapping, lots of compute was wasted and the detector was slow. Fast R-CNN improved this by passing the whole input image once via a CNN feature extractor and used a feature map internally to this CNN to elect proposals, therefore avoiding the feature extraction per proposal. Faster R-CNN removed the external dependency on proposal generation and introduced a Region Proposal Network (RPN) internally to the detector. For the RPN to generate proposals, prior (or anchor)  boxes were defined uniformly across the input image and the RPN was trained to predict the class of each anchor and by how much the anchor needs to shift to match the ground truth bounding box. 


## Implementation and Notebooks

The four notebooks in this section use Tensorflow. For Pytorch see [Detectron2](https://github.com/tensorflow/tpu/tree/master/models/official/detection) and [this tutorial](https://colab.research.google.com/drive/16jcaJoc6bCFAQ96jDe2HwtXj7BMD_-m5). 

* [This notebook](https://pantelis.github.io/artificial-intelligence/aiml-common/lectures/scene-understanding/semantic-segmentation/demo.ipynb) demos MaskRCNN.

* [This notebook](https://pantelis.github.io/artificial-intelligence/aiml-common/lectures/scene-understanding/semantic-segmentation/inspect_data.ipynb) visualizes the different pre-processing steps to prepare the training data.

* [This notebook](https://pantelis.github.io/artificial-intelligence/aiml-common/lectures/scene-understanding/semantic-segmentation/inspect_model.ipynb) goes in depth into the steps performed to detect and segment objects. It provides visualizations of every step of the pipeline.

* [This notebook](https://pantelis.github.io/artificial-intelligence/aiml-common/lectures/scene-understanding/semantic-segmentation/inspect_weights.ipynb) inspects the weights of a trained model and looks for anomalies and odd patterns.

