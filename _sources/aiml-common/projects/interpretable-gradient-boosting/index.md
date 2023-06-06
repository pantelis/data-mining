# Interpretable Gradient Boosting - Real Estate House Price Prediction


Ask a home buyer to describe their dream house, and they probably won't begin with the height of the basement ceiling or the proximity to an east-west railroad. But this playground competition's dataset proves that much more influences price negotiations than the number of bedrooms or a white-picket fence. With 79 explanatory variables describing (almost) every aspect of residential homes in Ames, Iowa, this competition challenges you to predict the final price of each home.


### Milestone 1: (Week 1, 10 points)

Set up a development environment in your laptop. Learn the basics of docker by watching the following video:

```{eval-rst}
.. youtube:: pTFZFxd4hOI
```

If you are on Windows you will need to follow [these instructions](https://docs.docker.com/desktop/windows/wsl/) and install [Docker Desktop](https://www.docker.com/products/docker-desktop) and [WSL2](https://docs.microsoft.com/en-us/windows/wsl/install-win10). 

Independent of your OS, you may want to use [VS Code IDE](https://code.visualstudio.com/) if you have no IDE experience before. 

Submit the github repository URL with a branch titled 'milestone-1' with the README.md file containing the installation instructions you followed and a screenshot of your docker container terminal prompt. Add as collaborator the TA.


### Milestone 2: (Week 3, 40 points)

Download the dataset from [here](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques/overview)

```{eval-rst}
.. youtube:: -taOhqkiuIo
```

Read the [excellent summary on SHAP that Google engineers have put together](https://storage.googleapis.com/cloud-ai-whitepapers/AI%20Explainability%20Whitepaper.pdf).  Watch the video and read the blog posts [here](https://towardsdatascience.com/interpretable-machine-learning-with-xgboost-9ec80d148d27) to understand the problem and its solution provided by [Tree SHAP](https://proceedings.neurips.cc/paper/2017/hash/8a20a8621978632d76c43dfd28b67767-Abstract.html). The blog post discusses the XGBoost implementation of gradient boosting but the concept is the same. 

Perform the SHAP interpretation of the house price prediction model of your choice. At a minimum you should produce graphs that show the SHAP values for the features and the SHAP interaction values for these features.


### Milestone 3: (Week 4, 30 points)

Merge the earlier branch into the main branch and create a new branch titled 'milestone-3. Do not delete the milestone-2 branch.

Repeat the analysis in Milestone 2 but this time use [this](https://towardsdatascience.com/kagglers-guide-to-lightgbm-hyperparameter-tuning-with-optuna-in-2021-ed048d9838b5) or [this](https://neptune.ai/blog/lightgbm-parameters-guide) guide to tune with [Optuna](https://optuna.org/) the hyperparameters of the LightGBM model.

You need to creating a streamlit app for the house price prediction problem. Streamlit is a python library that allows you to create web apps with minimal coding and deploy them in the cloud.  Deploy the streamlit app in [HuggingFace streamlit spaces](https://huggingface.co/docs/hub/spaces-sdks-streamlit) after you create a free account. The app must resemble [this UI](https://adhok-streamlit-ames-housing-price-predict-streamlit-app-lp8hyj.streamlit.app/) (please avoid the shown gif image) and in addition it must show a SHAP summary plot and a SHAP interaction plot. 

Submit the github repository URL with a branch titled 'milestone-3' with the README.md file containing the link to the deployed HF space where the Milestone 2 calculation and the optimized app calculation price prediction can both be seen. 

### Milestone 4: Documentation and Video Production (Week 5, 20 points)

Merge the earlier branch into the main branch and create a new branch titled 'milestone-4'. Do not delete the milestone-3 branch.

Document extensively both the code as well as the results (10 points). 

Use google sites to create a landing page for your app (5 points)

Create a video that will demonstrate the app. The video should be no longer than 5 minutes and should be either uploaded to your youtube channel or inlcuded in the github repository as an mp4 (5 points).

