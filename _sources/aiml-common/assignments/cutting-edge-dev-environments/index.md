# Cutting Edge Development Environment(s) 

The purpose of this assignment is to get you started in the course and to make sure that you have the necessary software installed on your computer. 

Minimal HW requirements: Later generation Macbook Pro or equivalent Windows or Linux laptop with at least 16GB of RAM and 512GB of SSD storage. 

Minimal SW Requirements: Although in the description below we may refer to VS Code similar facilities must be provided in PyCharm IDE.  

## Task 1 - Github and Docker background (10 points)

If you have no prior experience with Git or Docker, please watch the two [videos included in your course site](https://pantelis.github.io/data-mining/aiml-common/resources/environment/index.html). 

After you become familiar with these two technologies, please follow the instructions below to install Docker on your computer. Be careful to follow the instructions for your operating system as detailed in the section "On your own desktop or laptop" depending on the operating system. This is especially critical for Windows users that need to work with WSL2. 

Login to dockerhub and submit a screenshot of the `docker pull` command shown [here](https://hub.docker.com/_/hello-world). The screenshot must be in png format and  linked as an image in your README.md (markdown) file - see Task 3.


## Task 2 - Star and clone two Github repos (10 points)

No course or software project starts in vaccumm and you will be working with a variety of github repos. For this assignment, you will be working with two repos:

1. Course site repo: https://github.com/pantelis/data-mining
2. Hands on ML3: https://github.com/ageron/handson-ml3

Clone or Fork them. 

Ensure that you can launch at the very least the `handson-ml3` docker container and `attach` your VSCode IDE to it.   Use the GPU version of the Dockerfile if you have an NVIDIA GPU on your computer. If you have Intel or AMD GPUs chances are the `Dockerfile.gpu` will not work for you. All others, please use the CPU (`Dockerfile`) version.

Run [this notebook](https://github.com/ageron/handson-ml3/blob/main/01_the_machine_learning_landscape.ipynb) in the docker container using your VSCode IDE and save it (preserving all outputs). 

NOTE: The course is supported currently by two containers suitable for NVIDIA GPUs.  Those that have  NVIDIA GPUs will be able to edit the .devcontainer contents to point to either version of the container (pytorch or tensorflow) and automatically attach the VSCode to it. The attachment will build the course site if everything works. You are not required to do this for this assignment. 


## Task 3 - Create your own assignment repo (15 points)

Follow the video instructions [here](https://pantelis.github.io/data-mining/aiml-common/resources/environment/assignment-submission.html) to set yourself up for submitting this and other assignments. 

Copy the `docker` folder and the .gitignore file from the `handson-ml3` repo to the root of your repo. 

Your assignments repo must have a directory called `assignment-1` - all subsequent subtasks refer to this directory. 

1. Include in the `assignment-1` dir a README.md file with a link to png screenshot of Task 1. If you are not familiar with markdown syntax, please refer to [this tutorial](https://www.markdowntutorial.com/). Note that markdown is used in all software projects and your documentation currently limited to this README.md file must look good. Ensure that the README.md file is parsable by github.com and the screenshot is shown (5 points)

2. Copy the notebook of task 2  and successfully execute it in the container when this execution is triggered by the VSCode IDE. Save the output. This is a task identical to Task 2 but this is now happening in your own repo (5 points)

3. Push the changes to your repo and ensure that the github workflow is triggered and the results is a green checkmark. If this is happening your TA will be able to grade your assignment. (5 points) 
