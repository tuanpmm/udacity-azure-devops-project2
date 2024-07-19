# Overview

In this project, we will build a Github repository from scratch and create a scaffolding that will assist you in performing both Continuous Integration and Continuous Delivery. Next, we'll integrate this project with Azure Pipelines to enable Continuous Delivery to Azure App Service.

## Status Badge
[![Python application test with Github Actions](https://github.com/tuanpmm/udacity-azure-devops-project2/actions/workflows/pythonapp.yml/badge.svg)](https://github.com/tuanpmm/udacity-azure-devops-project2/actions/workflows/pythonapp.yml)

## Project Plan
In this section, we will create a Trello board for task tracking as well as a spreadsheet with the estimated project plan.

* A [Trello](https://trello.com/b/TYCfqOVA/azure-devops-task-tracking) board for tracking tasks of the project
* A project plan spreadsheet that includes in the `project-management-template.xlsx` file

## Architectural Diagram
![alt text](<evidences/Architectural Diagram.png>)

## Instructions

### Create a GitHub Repo
### Launch an Azure Cloud Shell environment and create ssh-keys
![alt text](<evidences/Launch an Azure Cloud Shell environment and create ssh-keys.png>)

### Upload these keys to GitHub account
![alt text](<evidences/Upload these keys to GitHub account.png>)

### Clone project from GitHub
![alt text](<evidences/Clone project.png>)

### Create the Makefile
```bash
install:
    pip install --upgrade pip &&\
        pip install -r requirements.txt

test:
    python -m pytest -vv test_hello.py


lint:
    pylint --disable=R,C hello.py

all: install lint test
```
### Create requirements.txt
```bash
Flask== 2.2.2
Werkzeug==2.2.2
pandas==1.3.5
numpy<2
scikit-learn==1.1.1
joblib==1.2.0
pylint==2.13.7
pytest==7.1.2
locust
```
### Create the Python Virtual Environment
```bash
python3 -m venv ~/.myrepo
source ~/.myrepo/bin/activate
```
### Create the script file and test file: `hello.py`, `test_hello.py`
```bash
# hello.py
def toyou(x):
    return "hi %s" % x


def add(x):
    return x + 1

def subtract(x):
    return x - 1
```
```bash
# test_hello.py
from hello import toyou, add, subtract

def setup_function(function):
    print("Running Setup: %s" % function.__name__)
    function.x = 10


def teardown_function(function):
    print("Running Teardown: %s" % function.__name__)
    del function.x

### Run to see failed test
#def test_hello_add():
#    assert add(test_hello_add.x) == 12

def test_hello_subtract():
    assert subtract(test_hello_subtract.x) == 9
```
### Run make all and make sure all tests passed
![alt text](<evidences/Run make all and make sure all tests passed.png>)

### Enable GitHub Actions in the GitHub UI
![alt text](<evidences/Enable GitHub Actions in the GitHub UI.png>)

### Replace yml code with scaffolding
```bash
name: Python application test with Github Actions

on: [push]

jobs:
build:

    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v4
    - name: Set up Python 3.9.19
    uses: actions/setup-python@v5
    with:
        python-version: 3.9.19
    - name: Install dependencies
    run: |
        make install
    - name: Lint with pylint
    run: |
        make lint
    - name: Test with pytest
    run: |
        make test
```
### Verify remote tests pass in GitHub Actions UI
![alt text](<evidences/Verify remote tests pass in GitHub Actions UI.png>)

### Add the GitHub actions badge to the README

### Deploy the app to an Azure App Service use command: `az webapp up -g Azuredevops -l "west europe" --sku F1 -n tuanpm14-azure-devops-project2`
![alt text](<evidences/Deploy the app to an Azure App Service.png>)

![alt text](<evidences/Create app service success.png>)

### Create and Authorize Azure App Service
  
* Go to [https://dev.azure.com](https://dev.azure.com) and sign in

* Create new project
    ![alt text](<evidences/Create new project.png>)

* Create new service connection
    ![alt text](<evidences/Create new service connection.png>)

* Create new Azure Pipelines
![alt text](<evidences/Create new Azure Pipelines.png>)

* Connect to GitHub
    ![alt text](<evidences/Connect to GitHub.png>)

* Approve to access repository
    ![alt text](<evidences/Approve to access repository.png>)

* Select an existing YAML file
    ![alt text](<evidences/Select an existing YAML file.png>)

* After setup Pipeline, push code to check result
    ![alt text](<evidences/After setup Pipeline, push code to check result.png>)

* Check result after deploy success by go to URL: [https://tuanpm14-azure-devops-project2.azurewebsites.net](https://tuanpm14-azure-devops-project2.azurewebsites.net)
    ![alt text](<evidences/Check result after deploy success.png>)

* Verify Prediction with Starter code file `make_predict_azure_app.sh`
    ![alt text](<evidences/Verify Prediction with Starter code file.png>)

### Load test an application using Locust with command: `locust -f locustfile.py --headless -u 20 -r 5 -t 10s`
![alt text](<evidences/Load test an application using Locust.png>)


## Enhancements

* Deploy application to AKS

## Demo 

[https://www.youtube.com/watch?v=ub13lDDtFH4](https://www.youtube.com/watch?v=ub13lDDtFH4)