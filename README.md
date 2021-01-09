# Capstone_Project3_AzureML_Nanodegree

## Overview Of Dataset
***
![alt text](https://raw.githubusercontent.com/AmDeep/Project2_Udacity_Microsoft_ML/main/Images/screen-shot-2020-09-15-at-12.36.11-pm.png)

The information in the dataset is stored in the comma separated values (CSV) format. This dataset represents the biological response of a Each row in this data set represents a molecule. The first column contains experimental data describing a real biological response; the molecule was seen to elicit this response (1), or not (0). The remaining columns represent molecular descriptors (d1 through d1776), these are caclulated properties that can capture some of the characteristics of the molecule - for example size, shape, or elemental constitution. The descriptor matrix has been normalized.


The objective of the competition is to help us build as good a model as possible so that we can, as optimally as this data allows, relate molecular information, to an actual biological response.

We have shared the data in the comma separated values (CSV) format. Each row in this data set represents a molecule. The first column contains experimental data describing an actual biological response; the molecule was seen to elicit this response (1), or not (0). The remaining columns represent molecular descriptors (d1 through d1776), these are calculated properties that can capture some of the characteristics of the molecule - for example size, shape, or elemental constitution. The descriptor matrix has been normalized.


The development of a new drug largely depends on trial and error. It typically involves synthesizing thousands of compounds that finally becomes a drug. This process is extremely expensive and slow. Therefore, the ability to accurately predict the biological activity of molecules, and understand the rationale behind those predictions would be of great value to the pharmaceutical industry. Gradient Boosting Machines (GBMs) are powerful ensemble learning techniques that have been successfully applied to several low-dimensional applications. Despite their high accuracy, GBMs suffer from major drawbacks such as high memory-consumption. In this paper, using real, high-dimensional (i.e. 1776 predictors) molecules dataset, we demonstrate that by using different feature selection/reduction techniques, the computations costs for building and tuning GBMs can be substantially reduced at a slight drop in prediction accuracy. In addition, by fusing the decisions made by the ensembles using two fusion techniques, namely a majority vote and an optimized feedforward neural network, we obtain a better prediction accuracy than the individual accuracy of all ensembles.
