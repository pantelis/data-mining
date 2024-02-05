# Your Programming Environment

## Compute

### On your own server/desktop machine or laptop (recommended)

You need to create Python environments in  this course. Nothing beats a container-based environment for data science/AI workflows. Learn the basics of docker (the most conmmon container format) by watching the following video:

```{eval-rst}
.. youtube:: pTFZFxd4hOI
```

Independent of your OS, you may want to use [VS Code IDE](https://code.visualstudio.com/) if you have no IDE experience before. We recommend VS Code as the IDE due to its flexibility in supporting remote containers.  Ensure that you are able to debug code in your IDE. It must connect to the [remote container](https://code.visualstudio.com/docs/remote/remote-overview). PyCharm may also offer similar functionality but we have not tested it.

* For those in Windows, please follow [this](https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-containers) to install WSL2 and Docker.

* For Mac users please follow the docker instructions [here](https://docs.docker.com/docker-for-mac/install/).

* For Ubuntu users please follow the docker instructions [here](https://docs.docker.com/engine/install/ubuntu/).

* For other linux users please follow the docker instructions [here](https://docs.docker.com/engine/install/).

For those that do not have an existing NVIDIA-based GPU, please avoid **buying** any AMD or Intel GPUs. Even to this date, the best way of workload acceleration is via CUDA and NVIDIA is obviously the only vendor that supports CUDA. Maybe one day we will have a true multivendor choice - its not today though.

If you do already have AMD or Intel GPUs you _may_ still be able to use them  or simply use Colab. 

#### Example Development Environment

An example environment is provided [here](https://github.com/pantelis/handson-ml3). This is a slightly modified environment based on [this book's repo](https://github.com/ageron/handson-ml3). In this environment you can launch the container from VS Code using a single click on the prompt 'Reponen in Container" if you have installed the remote container and docker extension.

### Google Colaboratory (recommended)

We will be using the **free** CPU/GPU resources provided by [Google Colab](https://colab.research.google.com). The good news is that you have an account in Google Colab as most of you have your university gmail account. Please note if you login to colab with your university account you get to use the almost unlimited Gdrive storage facility. You will need Google Colab for all your projects so that you can demonstrate that your results can be replicated.  In addition Colab has many [features](https://colab.research.google.com/notebooks/basic_features_overview.ipynb) that come handy. Please note that even if you use Colab, you still need to submit your work via Github i.e. you need to [connect Github and Colab](https://bebi103a.github.io/lessons/02/git_with_colab.html). 

### On AWS  (recommended)

Please note that the [AWS Deep Learning AMIs](https://docs.aws.amazon.com/dlami/latest/devguide/what-is-dlami.html) may not require installation or they may require update to the required version of TF/Pytorch. Choose this option if you can afford the hourly rate **and** you are disciplined to monitor the resources and terminate your instances.  

### On Hugging Face Spaces (recommended)

[HF spaces](https://huggingface.co/new-space?sdk=docker) can get you started for free and this includes docker based environments ! So it should be your first choice when an assignment or project requires container based development. 

### Kaggle (not recommended)

You can use Kaggle as an alternative to Colab for all your projects. You guessed it right - all the projects in this course are in fact Kaggle competitions.  You can login with your gmail account. You can install by following the directions [here](https://github.com/Kaggle/kaggle-api) the Kaggle command line interface (CLI).  Not only you will get to compete (your ranking relative to others does not matter per se), but as you improve your knowledge over time you can revisit these competitions and see how your score improves.  There is one catch though - Colab offers more GPU time and it comes with multiple tiers of service for a few dollars per month. This can be handy for the heavier projects.  

## Managing Python Runtimes

Follow the instructions [here](https://pipenv.pypa.io/en/latest/) to install pipenv. Managing dependencies is one of the key challenges in data science. Pipenv is a tool that helps you manage your dependencies.

Please ensure that you have set `PIPENV_VENV_IN_PROJECT=1` in your .env or .bashrc/.zshrc (or other shell configuration file) for creating the virtualenv (name it `.venv`) inside your project’s directory. **Do not commit the .venv folder in your Github repo - learn how to do that via the `.gitignore` file eg include [this file](https://www.toptal.com/developers/gitignore/api/python) in your git root folder**.


## Git / Github

Learning basic git commands takes less than half an hour. However, to install git and understand the principle behind git, please go over Chapters 1 and 2 of the [ProGit book](https://git-scm.com/book/en/v2).

As we have discussed in the class you need to be able to publish your work in Github so you need to create a Github account. Then you will use the git client for your operating system to interact with github and iterate on your projects.  Almost no project starts in vacuum - there is almost always a repo  that will neeed to be cloned and that you will need to modify to your needs. 

```{eval-rst}
.. youtube:: RGOj5yH7evk
```

### How to work with a github repository in Colab

1. Fork the desired repository if this is not yours. For example go to https://github.com/ageron/handson-ml3 and press the Fork button. 
2. After forking you should see the repository appearing in your account. 
3. Click the green button `Clone or download`, click Use HTTPS and copy the field with the location of the repo your forked. 
4. Go to https://colab.research.google.com/ and login with your university email account
5. In the window that pops up select Github. Accept the requested additional permission request for your university email account. After Github and Colab connects you will be able to see the forked repo from your drop down menu of Repository. You will also see all the notebooks that start with a number e.g 01_the_machine_learning_landscape.ipynb. The number indicates the chapter number. 
6. Select to open the 01-*.ipynb notebook by clicking on it. You should see the notebook in your own colab account. Any change will be persisted in your github. 
7. Run the first cell. If you havent used Notebooks before, people with little programming experience will fall in love with them especially at this stage where you dont need to type new code. For a tutorial on how to use the notebooks in colab or in general open and run the notebook [Welcome to Colaboratory](https://colab.research.google.com/notebooks/intro.ipynb).


## External Tools and Databases (Optional)

### Elastic Search Environment Setup

For project work you may need to install ES. Please note you are responsible for setting up the environment. For example to set up ES in Win10 you may follow [this](https://www.youtube.com/watch?v=hzaG2Uq60uw) guide but bear in mind that we cannot support any IT issues you may encounter in your laptop. You may decide to set up a development environment in AWS cloud 9 that is linux based for a small fee or taking advantage the free tier for _new_ AWS accounts (which is not free if you need EC2 instances outside of what the free tier provides).


