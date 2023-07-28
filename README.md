# NLP-Disaster-Tweets
The "NLP for Disaster Tweets" project aims to develop a machine learning model that can accurately distinguish between 
real tweets reporting genuine disaster events and tweets containing misleading or fake information about disasters. 
In times of emergencies, social media platforms like Twitter become crucial sources of information for authorities, 
relief organizations, and the public. However, these platforms are also prone to the spread of misinformation, which 
can lead to panic and hamper disaster response efforts.

The project will involve Natural Language Processing (NLP) techniques to preprocess and analyze textual data from tweets. 
The dataset used for training and evaluation will consist of labeled tweets, where each tweet is categorized as either 
a "real" disaster-related tweet or a "fake" non-disaster-related tweet.

## Introduction
In this project, we will use BERT (Bidirectional Encoder Representations from Transformers) to classify disaster tweets.
In the notebook `notebooks/01-bert-disasters-tweets.ipynb`, we will use the pre-trained BERT model from the Hugging Face Transformers library. The
notebook was used to create a training prototype, and the code was then refactored into a pipeline using Azure Machine Learning.

The src folder contains the code for the pipeline. The pipeline is defined in the `amls_pipeline` folder, and the components 
are defined in the `amls_components` folder. All the infrastructure is being built with the package `azureml-infra-tools`, it is my own package to help me build the infrastructure faster, 
you can check it out in the following link: https://github.com/H3NR1QU3M4LT4/azureml-infra-tools and also in PyPi: https://pypi.org/project/azureml-infra-tools/.
Also the configuration files are in the `conf` folder using hydra to manage the configuration files.

The `main.py` file is the entry point of the pipeline, and it is used to run the pipeline in the Azure cloud, using the Azure Machine Learning Studio.
After a successfully run of the pipeline, the model is registered in the Azure Machine Learning Studio, and it can be deployed as a web service. Also in
the job sections of the Azure Machine Learning Studio, you can see the metrics of the pipeline, and the metrics of the model.

## Data
The dataset used for this project is the [Real or Not? NLP with Disaster Tweets](https://www.kaggle.com/c/nlp-getting-started)
Check out the https://github.com/Kaggle/kaggle-api for more information about the Kaggle API, and how to install and use it.
To download the dataset, run the following command in the terminal:
```
cd data
kaggle competitions download -c nlp-getting-started
```

## Project Structure
```
├── data
│   ├── raw
│   │   ├── sample_submission.csv
│   │   ├── test.csv
│   │   └── train.csv
│   └── processed
│       ├── test.csv
│       └── train.csv
│       └── val.csv
├── models
│   └── ...
├── notebooks
│   └── ...
├── src
│   ├── amls_components
│   ├── amls_pipeline
│   ├── conf
│   ├── dependencies
│   ├── main.py
```

## Setup

Create a conda environment and install using the `environment.yml` file:
```
conda env create -f environment.yml
```

Activate the environment:
```
conda activate nlp-disaster-tweets
```

Then use poetry to install the project dependencies:
```
poetry install
```

You also will need to create a .env file in the root of the project, and add the following variables:
```
SUBSCRIPTION_ID=<Your Azure Subscription ID>
RESOURCE_GROUP_NAME=<Your Azure Resource Group>
WORKSPACE_NAME=<Your Azure Machine Learning Workspace Name>
```

## Run

To run the project, use the following command:
```
python src/main.py
```

If you are not using PyCharm, you need to add the following code in the `main.py` file:
```
import sys
sys.path.append("<AbsolutePath>/DistilDataQuarry/")
```

Change the <AbsolutePath> to the absolute path of the project folder in your local machine.

## Conclusion
The model achieved an accuracy of 0.9937107, a F1 score of 0.992181, and a ROC AUC score of 0.9963312. The model is performing very well,
The model can be improved by using a different model architecture, or test different hyperparameters, etc.

### Plots of the metrics
![alt text]()

### Tables of the metrics
![alt text]()