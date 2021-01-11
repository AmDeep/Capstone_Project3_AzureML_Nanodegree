# Capstone_Project3_AzureML_Nanodegree
***

## Overview Of Dataset
***
![alt text](https://st4.depositphotos.com/4687155/27336/v/600/depositphotos_273364926-stock-video-4k-hexagon-chemical-moleculardata-information.jpg)

The information in the dataset is stored in the comma separated values (CSV) format. Each row in the dataset represents a molecule while the first column titled Activity depcts the experimental data describing a real biological response. This is the output metric to measure and is dichotomous in nature with two possible values- the molecule was seen to elicit this response (1), or not (0). The dataset has 1776 input columns that describe molecular descriptors- from D1 to D1776. These columns relate to complex data about the molecules such as the size, shape, or elemental constitution. All elements in the descriptor matrix have been normalized.

This dataset has been sampled from Kaggle as part of a research study and is open source, making it viable for the use of this project. The objective of this project is therefore to define the best parameters and metrics for the most accurate of models, by connecting molecular information to the actual biological response. 
***

## Purpose & Objectives
***
The modelling of this dataset can vastly improve the detection and synthesis of drugs, reducing time and operational costs. Since the development of a new drug largely depends on trial and error by studying biological responses to new substances, industries largely focus on augmenting such detection processes. The several compounds once synthesized, become drugs through a process that is extremely expensive and time-consuming. It is common in the industry for companies to finance large scale pharmaceutical products to no effect as the desired products may never be detected, let alone produced.

One of major objectives of this project is to thus accurately predict the biological activity of molecules, and understand the rationale behind those predictions as a method of imparting value to the pharmaceutical industry. Current industry standards stress on the use of Gradient Boosting Machines (GBMs) for achieving the desired results. These robust ensemble learning techniques may offer high accuracies, but are highly memory intensive and can rarely be applied for other substances and drugs. By using both the hyperdrive grid searching methods and AutoML configurations, this capstone project will perform a comparative study of the maximum possible accuracy achieved through different methods. Emphasis will also be placed on the feature selection techniques of AutoML and the deployment of models throug Swagger an ACI. Due to the dichotomous nature of the output metric, a classification scheme has been used for AutoML and logistic regression for the grid searches through hyperdrive configuration.
***

## Hyperdrive Modelling
***
In order to perform a hyperdrive search, we begin by first creating a compute instance and generating code on Jupter Notebooks. The training and testing dataset are imported directly in their raw forms and then converted to tabular datasets. These are then converted to dataframes using pandas. The necessary libraries are imported and a sample experiment is created in the workspace. A cpu cluster is named and created with a certain vm size and 5 maximum nodes. One notebook uses ScriptRunConfig and the notebook in the Final folder uses a deprecated version of SKLearn.
By defining a configuration for the logistic regression test, we apply different paramteric tests for the C value(inverse of regularization strength) and maximum iterations. We define a policy using BanditPolicy with a slack factor, evaluation intervals and evaluation delay. The primary metric is set to accuracy, which has to be maximized. A total of 150 runs are specified and 5 maximum cocurrent runs.
The code for training is stored in the train.py file. After executing the run on the environment, we arrive at the following configuration with the best accuracy:-

***************************************************************************************************************************
### Best Run ID:-  HD_012aba72-78a4-4a4d-92fd-aca87c3320b1_3

### Metrics:-  {'Regularization Strength: ': 0.1, 'Max iterations: ': 64, 'Accuracy': 0.7656500802568218}

### Parameters:-  ['--C', '0.1', '--max_iter', '64']

### Accuracy:-  0.7656500802568218
***************************************************************************************************************************

![alt text](https://raw.githubusercontent.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/FinalHyperDriveFiles/hdc1.PNG)

![alt text](https://raw.githubusercontent.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/FinalHyperDriveFiles/hdc2.PNG)
![alt text](https://raw.githubusercontent.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/FinalHyperDriveFiles/hdc3.PNG)

The outputted best model is stored under hyperdrive_best_model.joblib and the successful status of the runs can be seen from the images above.

***

## AutoML Modelling
***
A score.py file is created with commands for telemtry, input sampling and output sampling. This is achieved by applying a pandas Series setup. Further commands are inputted in the file to create environments and load models once AutoML outputs the best results. Three of the most accurate models as seen from the images below are:-
### 1. VotingEnsemble-----------------------------------> 0.8131
### 2. StackEnsemble------------------------------------> 0.8105
### 3. StandardScalerWrapper XGBoostClassifier----------> 0.8081
![alt text](https://github.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/FinalAutoMLFiles/AUTOMLNANODEGREE.PNG)
![alt text](https://github.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/FinalAutoMLFiles/AUTOMLPAGE2.PNG)
![alt text](https://github.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/FinalAutoMLFiles/AUTOMLPAGE3.PNG)
![alt text](https://github.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/FinalAutoMLFiles/AUTOMLPAGE6.PNG)


The details for the run and the respective metrics such as AUC, accuracy, losses can be compared from the images above. The information for the Voting Ensemble algorithms and weights can be summarized as per below:-
**************************************************************************************************************************

### {'_aml_system_azureml.automlComponent': 'AutoML', '_aml_system_ComputeTargetStatus': '{"AllocationState":"steady","PreparingNodeCount":0,"RunningNodeCount":1,"CurrentNodeCount":5}', 'ensembled_iterations': '[6, 0, 22, 9, 10, 1, 18, 24, 25]', 'ensembled_algorithms': "['XGBoostClassifier', 'LightGBM', 'LightGBM', 'XGBoostClassifier', 'XGBoostClassifier', 'XGBoostClassifier', 'LightGBM', 'LightGBM', 'XGBoostClassifier']", 'ensemble_weights': '[0.07142857142857142, 0.07142857142857142, 0.2857142857142857, 0.14285714285714285, 0.14285714285714285, 0.07142857142857142, 0.07142857142857142, 0.07142857142857142, 0.07142857142857142]', 'best_individual_pipeline_score': '0.8080553191489361', 'best_individual_iteration': '6', '_aml_system_automl_is_child_run_end_telemetry_event_logged': 'True'}
![alt text](https://github.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/FinalAutoMLFiles/AUTOMLPAGE7.PNG)
***************************************************************************************************************************

***

## Deployment & Endpoint Results
***
Using Azure ACI, a webservice can be deployed as seen from the images below where we define sample values for the all inputs(from D1 to D1776). This input data is converted to a JSON format and dumped. In the endpoint.py file, we set the content type and fill in the Scoring URI obtained from the ACI webservice model deployment. Once the respective model endpoint has a healthy status, we can then send sample inputs to test out the output through two separate methods:-
1. By running the endpoint.py file with predefined input sample points.
2. Creating a sample JSON file and deploying the model on it, in order to compare the true and predicted outputs.
![alt text](https://github.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/FinalAutoMLFiles/AUTOMLPAGE4.PNG)
![alt text](https://github.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/FinalAutoMLFiles/AUTOMLPAGE5.PNG)
![alt text](https://github.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/FinalAutoMLFiles/DEPLOYMENT.PNG)
![alt text](https://github.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/FinalAutoMLFiles/MODELDEPLOYAUTOML.PNG)
As per the results obtained from the images above, we can see that the predicted and true values closely match for the sample inputs, signifying that the model deployment is successful. The model endpoint is deleted once the program objectives are achieved.
***

## Swagger JSON and UI
***
The concept of the model deployment is expanded to a sample application through Swagger. This UI and model deployment is performed on a separate lab environment due to the lack of time on the initial lab environment, owing to long model development periods and slower connectivity. Using a similar code for the endpoint, we execute commands through docker to implement modules for JSON, shell, configuration, benchmark and log scripts. The end result is a working local host application that visualizes the individual input metrics and also allows the files to be used on sample inputs. 
![alt text](https://github.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/Data/Swagger1.PNG)
![alt text](https://github.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/Data/Swagger2.PNG)
![alt text](https://github.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/Data/Swagger3.PNG)
![alt text](https://github.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/Data/Swagger4.PNG)
![alt text](https://github.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/Data/Swagger5.PNG)
![alt text](https://github.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/Data/Swagger6.PNG)

The images above show the results of the scripts and the model endpoints, indicated by the [true.true] output. Server response times and the resultant execution periods can be ascertained from the remaining swagger data. The model endpoint is deleted through the console once the objectives are met. Further explanation on the steps has been provided in the video.
***
## Recommendations & Future Steps
***
The determination of molecular data for the purpose of synthesizing molecular data is hugely dependent on the calculation of thousands of datapoints. It is more imperative for these calculations to be accurate and time sensitive in order to avoid projects becoming overtime and overbudget. Current highest accuracies that have been achieved through Kaggle experts, gives us a glimpse of how problematic this issue is, with average values being ~30% to 35%. The results of this project prove that it is possible to improve these scores and even compare the best models against each other.

The model depolyments can be made more user friendly and intuitive by the inclusion of better buttons and icons for the Swagger file. This can also be linked with a light weight Flask application for better operability. Further feature engineering can also be performed on the individual columnar values to derive better predictors for the output to raise the accuracies above 90%. Data denoising can also be performed to cut down on the values for the datasets that might deviate the models from better accuracies. Some of the columns represent signal values which can be preprocessed or redefined using feed forward transform filters. Other recommendationas and future steps include:-

1. Focusing on better UI and augmented response for users.
2. Connecting activity(output) results with visuals to help improve data interpretation.
3. Performing grid search tests on other parameters other than regularization strength and maximum number of iterations.
4. Performing PCA and t-SNE plot tests on the data to interpret the relationship between inputs and outputs.
5. Using the timeit() function to test out out fast the models respond to network deployments and output results.

***

## Video Link
***
Note:- Time stamps during different portions of the code and the video can differ because the project was performed on multiple virtual machines at different time periods.
https://youtu.be/wQQZhIhLKQc
***
