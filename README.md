# AzureProject2
# Building a CI/CD Pipeline Project: Deploy Flask Application using GitHub Actions and Azure CI/CD Pipelines

### Status Badge

[![Python Flask Application with Github Actions](https://github.com/Syedahmad75/Udacity-Bosch-CICD/actions/workflows/pythonapp.yml/badge.svg)](https://github.com/Syedahmad75/Udacity-Bosch-CICD/actions/workflows/pythonapp.yml)

### Overview
In this project, we build a Github repository from scratch and create a scaffolding that will assist us in performing both Continuous Integration and Continuous Delivery. we use Github Actions along with a Makefile, requirements.txt and application code to perform an initial lint, test, and install cycle. Next, we integrate this project with Azure Pipelines to enable Continuous Delivery to Azure App Service.
This project consists of flask application that is developed to predict housing prices in Boston. This project could be extended to any pre-trained machine learning model, such as those for image recognition and data labeling.

   
### Getting Started
1. Clone this repository 

2. Install the dependencies below

3. Create your own CI-CD Pipeline, follow the instructions below



### Dependencies
1. Create an [Azure Account](https://portal.azure.com) 
2. Use [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview)
3. Create [Azure Devops Account](https://azure.microsoft.com/en-us/services/devops/?nav=min)
4. Create [Self Hosted Agent in your PC](https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/agents?view=azure-devops&tabs=browser)





### Instructions
1. Switch to New Directory
2. `cd Azure`
3. Create a Virtual Environment
4. `python -m venv ~/.Azure` 
5. Activate the Virtual Environment
6. `source ~/.Azure/bin/activate`
7. Install dependencies in the virtual environment and run tests using `make all` command:
9. Uncomment line no 16 and 17 in test_hello.py file to see failed testcases
 ![failed-test-cases]
10. CI: Configure GitHUB Actions
    Enable Github Actions
    Go to your Github Account and enable Github Actions.
11. Replace yml code with scaffolding if it's not already there. 
    ```
    name: Python application test with Github Actions

    on: [push]

    jobs:
     build:

        runs-on: ubuntu-latest

        steps:
        - uses: actions/checkout@v2
        - name: Set up Python 3.7
          uses: actions/setup-python@v1
          with:
            python-version: 3.7
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
12. GitHub Actions Build Passed ![Github Actions]
13. Deploy the app to an Azure App Service
    - `az webapp up -n flaskapp-udacity -g FlaskApp-RG`


14. Now we need to create a Pipeline on Azure Devops. Steps are as follows. 
    1.  Go to https://dev.azure.com and sign in.
    2.  If more than one organization is listed, select the one you want to use for this tutorial. By default, Azure DevOps creates a new organization using the email alias you used to sign in.
    3.  If your organization doesn't have any projects, enter the project name Flask Pipelines under Create a project to get started, and then select Create project.
    4. From your project page left navigation, select Pipelines.\
    5. Select Create Pipeline:\
    6. On the Where is your code screen, select GitHub. You may be prompted to sign into GitHub.\
    7. On the Configure your pipeline screen, select Python to Linux Web App on Azure.
    Your new pipeline appears. When prompted, select the Azure subscription in which you created your Web App.

       - Select the Web App
       - Select Validate and configure
    8.  Azure Pipelines creates an azure-pipelines.yml file that defines your CI/CD pipeline as a series of stages, Jobs, and steps, where each step contains the details for different tasks and scripts. Take a look at the pipeline to see what it does. Make sure all the default inputs are appropriate for your code.

9. After Setup the CI-CD Workflow, push the code to check pipeline. Every Push Event will trigger a new CI-CD pipeline and your webapp will update accordingly. 

10. Check the Deployment by hitting the URL.In my case https://flaskapp-udacity.azurewebsites.net/. \

11. Verify Prdiction with Starter code file `make_predict_azure_app.sh`. (modify with your app name)
    1.  To make a prediction, you have to open a separate tab or terminal window. In this new window, navigate to the main project directory (some computers will do this automatically) and call `./make_prediction.sh` if testing locally, or modify `make_predict_azure_app.sh`.
    2.  This shell script is responsible for sending some input data to your application via the appropriate port. Each numerical value in here represents some feature that is important for determining the price of a house in Boston. The source code is responsible for passing that data through a trained, machine learning model, and giving back a predicted value for the house price.
    3.  In the prediction window, you should see the value of the prediction, and in your main window, where it indicates that your application is running, you should see some log statements print out. You’ll see that it prints out the input payload at multiple steps: when it is JSON and when it’s been converted to a DataFrame and about to be scaled.\
12. use locust to do a load test against our application.Replace '< yourappname >' in the provided configuration and call locust.\
    Using the parameters above locust will use 20 users with a spawn rate of 5 users per second and run for 20 seconds.\
    `locust -f locustfile.py --headless -u 20 -r 5 -t 5s`

### Enhancements
1. Create a UI with a button to predict the outcome. 
2. Custom Autoscale plan can be created for automated scaling based on load. 

### Youtube Video Link
[Youtube Video](https://www.youtube.com/watch?v=iEaqX4vwH68)
   
