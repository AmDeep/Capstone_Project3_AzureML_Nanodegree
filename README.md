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
 
![alt text](https://github.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/FinalHyperDriveFiles/hdc1.PNG)
![alt text](https://github.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/FinalHyperDriveFiles/hdc2.PNG)
![alt text](https://github.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/FinalHyperDriveFiles/hdc3.PNG)

The outputted best model is stored under hyperdrive_best_model.joblib and the successful status of the runs can be seen from the images above.

***

## AutoML Modelling
***
![alt text](https://github.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/FinalAutoMLFiles/AUTOMLNANODEGREE.PNG)
![alt text](https://github.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/FinalAutoMLFiles/AUTOMLPAGE2.PNG)
![alt text](https://github.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/FinalAutoMLFiles/AUTOMLPAGE3.PNG)
![alt text](https://github.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/FinalAutoMLFiles/AUTOMLPAGE4.PNG)
![alt text](https://github.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/FinalAutoMLFiles/AUTOMLPAGE5.PNG)
![alt text](https://github.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/FinalAutoMLFiles/AUTOMLPAGE6.PNG)
![alt text](https://github.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/FinalAutoMLFiles/AUTOMLPAGE7.PNG)
***

## Deployment & Endpoint Results
***
![alt text](https://github.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/FinalAutoMLFiles/DEPLOYMENT.PNG)
![alt text](https://github.com/AmDeep/Capstone_Project3_AzureML_Nanodegree/blob/main/FinalAutoMLFiles/MODELDEPLOYAUTOML.PNG)
***

## Recommendations & Future Steps
***

***

## Video Link
***

***
