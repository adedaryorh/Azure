# AzureProject2
# Building a CI/CD Pipeline Project: Deploy Flask Application using GitHub Actions and Azure CI/CD Pipelines

Project Plan
Trello board for task tracking as well as a spreadsheet with the estimated project plan.
A Trello board keep track of the tasks.
link: https://trello.com/invite/b/jASHAofS/ATTI9b2e7e9fc4caede4fd97eeec2151db37B074142F/flaskcicd
A Project Planning Spreadsheetspreadsheet has been created to manage the project schedule.
Link: https://docs.google.com/spreadsheets/d/1fi1APWukVy7KuaN8mI1WrVUaAa3ykESTGA8-DMCY7ro/edit?usp=sharing

### Status Badge

[![Python Flask Application with Github Actions]


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

Architectural Diagram
![image](https://github.com/adedaryorh/Azure/assets/64752771/2e23eece-b807-44d6-aee7-6d81f2c9dc63)


### Instructions
1. Switch to New Directory
2. `cd Azure`
https://drive.google.com/file/d/1dFheRhp2U8kWmEp35IdtXgoYSk86C_CL/view?usp=sharing
4. Create a Virtual Environment
`python -m venv ~/.Azure` 
https://drive.google.com/file/d/1tDTBY8YLiOxoAwo9fmIF0RhVMdDmfvom/view?usp=sharing
6. Activate the Virtual Environment
7. `source ~/.Azure/bin/activate`
8. Install dependencies in the virtual environment and run tests using `make all` command:
https://drive.google.com/file/d/1yOZrLNFw9OcYT3HeTjCppv_ohXcIXppw/view?usp=sharing
10. Uncomment line no 16 and 17 in test_hello.py file to see failed testcases
 ![failed-test-cases]
 https://drive.google.com/file/d/1p3Un9dKQdDpQKcPU1WXs5Jq-zej-nnYo/view?usp=sharing
10. CI: Configure GitHUB Actions
    Enable Github Actions
    (https://github.com/adedaryorh/Azure/assets/64752771/f331b686-190f-49d2-b86d-524673aeb222)

    Go to your Github Account and enable Github Actions.
    https://drive.google.com/file/d/17AgVTo0lgxqqfVdxPEGP0viPDhPA-Kni/view?usp=sharing
    https://drive.google.com/file/d/1g0ovaelmGekd8KqSv8j-AKREylxK1DaI/view?usp=sharing
    
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

14. Deploy the app to an Azure App Service
    - `az webapp up -n flaskapp-udacity -g FlaskApp-RG`
    


14. Now we need to create a Pipeline on Azure Devops. Steps are as follows. 
    1.  Go to https://dev.azure.com and sign in.
    2.  If more than one organization is listed, select the one you want to use for this tutorial. By default, Azure DevOps creates a new organization using the email alias you used to sign in.
    3.  If your organization doesn't have any projects, enter the project name Flask Pipelines under Create a project to get started, and then select Create project.
    ![image](https://github.com/adedaryorh/Azure/assets/64752771/01984232-74df-41aa-9d1b-5bb8e60cf98d)

    5. From your project page left navigation, select Pipelines.\
   https://drive.google.com/file/d/1dFu4zO0NAiRmsNhl_3S62Dg23bG_fjxq/view?usp=sharing
    7. Select Create Pipeline:\
    (https://github.com/adedaryorh/Azure/assets/64752771/0c08d10a-9da6-49bd-ab8b-3afbe8152dcd)

    8. On the Where is your code screen, select GitHub. You may be prompted to sign into GitHub.\
    (https://github.com/adedaryorh/Azure/assets/64752771/ceae4e93-a2f9-4546-a075-9bf62bc8cbef)

    9. On the Configure your pipeline screen, select Python to Linux Web App on Azure.
    Your new pipeline appears. When prompted, select the Azure subscription in which you created your Web App.

       - Select the Web App
       - Select Validate and configure
       https://drive.google.com/file/d/1dFu4zO0NAiRmsNhl_3S62Dg23bG_fjxq/view?usp=sharing
    8.  Azure Pipelines creates an azure-pipelines.yml file that defines your CI/CD pipeline as a series of stages, Jobs, and steps, where each step contains the details for different tasks and scripts. Take a look at the pipeline to see what it does. Make sure all the default inputs are appropriate for your code.

9. After Setup the CI-CD Workflow, push the code to check pipeline. Every Push Event will trigger a new CI-CD pipeline and your webapp will update accordingly. 
https://drive.google.com/file/d/1tcrAup1r_qdoX187aYjOCcQaz9mJ5cHi/view?usp=sharing
https://drive.google.com/file/d/1iHnW7P_wzdCjYDIwP54Yq68hxnNEnkoJ/view?usp=sharing
https://drive.google.com/file/d/10yWd44Pom9Jmc2q4-VKIC0_ZCwkep17H/view?usp=sharing
https://drive.google.com/file/d/19ZOKw-k0MqLrDlrFTc-399AAYazfEdhY/view?usp=sharing


10. Check the Deployment by hitting the URL.In my case https://adex-flaskapp-udacity.azurewebsites.net/. \
https://drive.google.com/file/d/1XcD2zXMaqZSF3kt6IVqnAUe0XLGzbUap/view?usp=sharing

11. Verify Prdiction with Starter code file `make_predict_azure_app.sh`. (modify with your app name)
    1.  To make a prediction, you have to open a separate tab or terminal window. In this new window, navigate to the main project directory (some computers will do this automatically) and call `./make_prediction.sh`
    https://drive.google.com/file/d/1utV99CNMBd2rz0jydHm3j2blGP3a6WEV/view?usp=sharing
    
    3.   if testing locally, or modify `make_predict_azure_app.sh`.
    4.  This shell script is responsible for sending some input data to your application via the appropriate port. Each numerical value in here represents some feature that is important for determining the price of a house in Boston. The source code is responsible for passing that data through a trained, machine learning model, and giving back a predicted value for the house price.
    5.  In the prediction window, you should see the value of the prediction, and in your main window, where it indicates that your application is running, you should see some log statements print out. You’ll see that it prints out the input payload at multiple steps: when it is JSON and when it’s been converted to a DataFrame and about to be scaled.\
12. use locust to do a load test against our application.Replace '< yourappname >' in the provided configuration and call locust.\
    Using the parameters above locust will use 20 users with a spawn rate of 5 users per second and run for 20 seconds.\
    `locust -f locustfile.py --headless -u 20 -r 5 -t 5s`
    https://drive.google.com/file/d/1LOpLseNyrIQFx-SnVr7QG2uwaR8z-gmL/view?usp=sharing

### Enhancements
1. Create a UI with a button to predict the outcome. 
3. Custom Autoscale plan can be created for automated scaling based on load. 
(https://github.com/adedaryorh/Azure/assets/64752771/c26300f9-12e2-4a81-b913-bdd210d4c7a8)
(https://github.com/adedaryorh/Azure/assets/64752771/83c0e654-3316-4f74-870d-031ad84b35b1)



### Youtube Video Link
(https://youtu.be/v0g-L1vi3cA)
   
