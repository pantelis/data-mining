---
title: ML Pipelines 
---

# ML Pipelines 

As we have seen from the syllabus, this course approaches the subject from an applied perspective - this means teaching concepts but at the same time looking how these concepts are applied in the industry to solve real world problems. In this respect here we take an architecture driven approach, presenting the components in a form of a software stack but also how the components are mechanized in what we call **Pipelines** to provide the required utility to applications. For a complete overview of real world ML pipelines used today we will go through [this paper that describes a production grade pipeline](http://stevenwhang.com/tfx_paper.pdf).

![AI stack](images/ai-stack.png)*AI Stack circa 2019*

## The four pipelines of an end-to-end ML platform

![E2E ML Pipeline](images/acumos-E2E.svg)
*Example of end to end pipeline - serial arrangement*

![Data Pipeline](images/acumos-DP1.svg)
*Example of Data Pipeline (DP)*

![Model Training Pipeline](images/acumos-MTP.svg)
*Example of Model Training Pipeline (MTP)*

![Model Evaluation and Validation Pipeline](images/acumos-MEVP.svg)
*Example of Model Evaluation and Validation Pipeline (MEVP)*

![Serving Pipeline](images/acumos-SP.svg)
*Example of Serving Pipeline (SP)*

## Roles in data science product development

![Data scientists and other actors](images/acumos-actors.svg)
*Who data scientists need to interact with, during the development of AI systems?*

> "Any organization that designs a system (defined broadly) will produce a design whose structure is a copy of the organization's communication structure." http://www.melconway.com/Home/Conways_Law.html

"We do research differently here at Google. Research Scientists aren't cloistered in the lab, but instead they work closely with Software Engineers to discover, invent, and build at the largest scale."

Contrast this to an organizational structure that isolates researchers from product development.  What about Alphabet's X https://x.company/ ?

## Landscape of the data science ecosystem
Due to the complexity and common interest to addresses industrial players are partnering to define and implement the necessary components for the complete automation of AI pipelines.  This work is going in within the [Linux Foundation AI (sub)Foundation](https://landscape.lfai.foundation/fullscreen=yes) amongst many other open source communities.

<section class="bg-apple">
              <div class="wrap">
          <iframe width="2120" height="630" src="https://landscape.lfdl.io/format=landscape&fullscreen=yes" frameborder="0" allowfullscreen></iframe>
          </div>
</section>

