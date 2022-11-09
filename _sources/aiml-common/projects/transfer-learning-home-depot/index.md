# Transfer Learning for Custom Datasets in the Small-Data Regime

This project will walk you through the development of a complete transfer learning pipeline from annotation to producing performance results of a network that performs semantic segmentation in the so called small data regime i.e. when the annotated examples per category are very few.  

You have been hired in the data science team at Home Depot and you are tasked to semantically segment objects shown in the so called "buyers guide" videos. You are to segment only objects that their customers can purchase in their stores. 

**If you miss a milestone deadline you will be forfeited the corresponding points.**

## Milestone 1: Environment Preparation (10 points)

In this stage you will be working with CVAT - you need to install CVAT locally to your laptop/desktop and we urge you to follow the docker setup instructions [here](https://opencv.github.io/cvat/docs/administration/basics/installation/)

PS: You can also create an account on the cvat.ai site but we dont offer any guarantees that the project can be delivered in its entirety with a cvat instance that is not managed by you. 

Submit a github repository with a branch titled 'milestone-1' with the readme file containing the CVAT installation instructions you followed and a screenshot of your computer of the login screen. Add as collaborator the TA.

## Milestone 2: Data Acquisition (20 points)

1. Go to the [HD site](https://www.homedepot.com/c/alp/diy-projects-and-ideas-ab/azzz-ab) and in the left panel select the home area (room) you have been assigned: 

    1. [kitchen](https://www.youtube.com/watch?v=cc0Sy4VpfT0) 
    2. [bathroom](https://www.youtube.com/watch?v=-Nkm58wSiKg) 
    3. [bedroom](https://www.youtube.com/watch?v=2mnShtGjRXM), 
    4. [garage](https://www.youtube.com/watch?v=AvKxzw5bjuc), 
    5. [basement](https://www.youtube.com/watch?v=gdcFrD-7hcI).
   
Project Team 1 is assigned home area 1 (Kitchen) just like Project Team 6, Project Team 3 is assigned home area 3 (Bedroom) just like Project Team 8 and so on ... 

2. Select 10 product categories (eg sinks, faucets) that HD sells in each room and that are shown on their promotional video 

```{eval-rst}
.. youtube:: poup0NZ2D40
```


2. You will need to scrape using [beautiful soup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/) or retrieve using the [Google Custom Search API](https://developers.google.com/custom-search/v1/overview) (better solution), 100 images of each of the selected product categories. Make sure you select products that are not included on the video, meaning if a specific sink is shown on the video, you srape / search different but similar sinks. 

Submit a Github branch titled 'data-acquisition' and a markdown file called data-acquisition.md containing the code that achieve the milestone and a `pytest` test  file that can show that the code works. 

## Milestone 3: Annotation (20 points)

1. Upload the images in your CVAT instance and annotate all object categories. This is a manual step and you will need to use the [DEXTR cutter](https://cvlsegmentation.github.io/dextr/). 

2. Write a 2 page summary on how DEXTR works that can be understood by experts. 

Ensure that the annotations can be read and seen by the [fiftyone tool](https://voxel51.com/docs/fiftyone/tutorials/cvat_annotation.html)

Submit a Github branch titled 'annotation' containing the annotated dataset in MS COCO format and a markdown file called annotation.md containing the DEXTR description and the link with the 1000 annotated images (10 product categories x 100 images per category. You can collaborate with other teams on the annotation task to share the load. 

## Milestone 4: Semantic Segmentation (40 points)

Use [this](https://github.com/ashleve/lightning-hydra-template) template or an equivalent template if you are using Tensorflow to implement a semantic segmentation pipeline based on either MaskRCNN (project team number is odd number) or UNet (project team number is even)  that will successfully segment the selected objects on the input room video.

You can use frameworks such as https://github.com/facebookresearch/detectron2 for this task. 

Ensure you describe how you tuned and what values you ended up using for the [network hyperparameters](https://medium.com/analytics-vidhya/taming-the-hyper-parameters-of-mask-rcnn-3742cb3f0e1b)

Submit a Github branch titled 'segmentation' containing  the segmentation code and a  markdown file called segmentation.md containing the full description of the semantic segmentation network you used and the performance results you got. 


## Milestone 5: Documentation (10 points) 

Use [Jupyterbook](https://jupyterbook.org/en/stable/intro.html) to bundle together all the markdown files and publish the project in html - do not commit your html build in github.

Include a copy of the produced video in your Github, showing the segmentations in real time. 

Ensure that you merge all the branches into main branch and submit the main branch  as the final project deliverable. 

PS: You can upload it to your youtube channel and link it to your Github profile if you like.  






