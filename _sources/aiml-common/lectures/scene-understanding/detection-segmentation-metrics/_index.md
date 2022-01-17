---
title: Object Detection and Semantic Segmentation Metrics
---

# Object Detection and Semantic Segmentation Metrics

NOTE: The following example was copied from [here](https://www.mdpi.com/2079-9292/10/3/279)

In this section we provide some intuition as to why we need additional metrics for detection and segmentation of objects.  As shown below such metrics are routinely used to compare various networks and approaches and manifest the progress that was made in the field over the last few years. 

![object-detection-performance](images/object-detection-performance.png)
_Detection performance_


## A practical example

Considering the set of 12 images in the figure below:

<!--- Toy example figure --->
<p align="center">
<img src="images/toy_example_mosaic.png" align="center" width="1000"/>
</p>

Each image, except (a), (g), and (j), has at least one target object of the class *cat*, whose locations are limited by the green rectangles.
There is a total of 12 target objects limited by the green boxes. Images (b), (e), and (f) have two ground-truth samples of the target class.
An object detector predicted 12 objects represented by the red rectangles (labeled with letters *A* to *L*) and their associated confidence levels are represented in percentages. Images (a), (g), and (j) are expected to have no detection. Conversely, images (b), (e), and (f) have two ground-truth bounding boxes.

To evaluate the precision and recall of the 12 detections it is necessary to establish an IOU threshold *t*, which will classify each detection as TP or FP.
In this example, let us first consider as TP the detections with *IOU > 50%*, that is *t=0.5*.

<!--- Toy example table t=0.5 --->
<p align="center">
<img src="images/table_1_toyexample.png" align="center" width="700"/>
</p>

As stated before, AP is a metric to evaluate precision and recall in different confidence values. Thus, it is necessary to count the amount of TP and FP classifications given different confidence levels.

By choosing a more restrictive IOU threshold, different precision x recall values can be obtained. The following table computes the precision and recall values with a more strict IOU threshold of *t = 0.75*. By that, it is noticeable the occurrence of more FP detections, reducing the recall.

<!--- Toy example table t=0.75 --->
<p align="center">
<img src="images/table_2_toyexample.png" align="center" width="720"/>
</p>

Graphical representations of the precision x values presented in both cases *t= 0.5* and *t=0.75* are shown below:

<!--- Curves t=0.5 and t=0.75 --->
<p align="center">
<img src="images/precision_recall_curve_toyexample.png" align="center"/>
</p>


By comparing both curves, one may note that for this example:

1) With a less restrictive IOU threshold (*t=0.5*), higher recall values can be obtained with the highest precision. In other words, the detector can retrieve about *66.5%* of the total ground truths without any miss detection.
2) Using *t=0.75*, the detector is more sensitive with different confidence values. This is explained by the amount of ups and downs of the curve.
3) Regardless the IOU threshold applied, this detector can never retrieve *100%* of the ground truths (recall = 1). This is due to the fact that the algorithm did not predict any bounding box for one of the ground truths in image (e).

Different methods can be applied to measure the AUC of the precision x recall curve. Considering the *N-point interpolation* to calculate the AP with *N=11*, the interpolation measures the recall in the points L=[0, 0.1, 0.2, 0.3, 0.4, 0.5, 0.6, 0.7, 0.8, 0.9, 1.0], and considering the *All-point interpolation* approach, all points are considered. Both approaches result in different plots as shown below:


<!--- Interpolating curves --->
<p align="center">
<img src="images/interpolations_toyexample.png" align="center"/>
</p>

When an IOU threshold *t=0.5* was applied (plots of the first row in image above), the 11-point interpolation method obtained *AP=88.64%* while the all-point interpolation method improved the results a little, reaching *AP=89.58%*. Similarly, for an IOU threshold of *t=0.75%* (plots of the second row in image above), the 11-point interpolation method obtained *AP=49.24%* and the all-point interpolation *AP=50.97%*.

In both cases, the all-point interpolation approach considers larger areas above the curve into the summation and consequently obtains higher results.
When a lower IOU threshold was considered, the AP was reduced drastically in both interpolation approaches. This is caused by the flexibility the threshold brings in considering TP detections.
