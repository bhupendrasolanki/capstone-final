*NOTE:* This file is a template that you can use to create the README for your project. The *TODO* comments below will highlight the information you should be sure to include.

# Heart Failure Prediction
## Project overview:

This project presents an opportunity to apply the knowledge gained from the Nanodegree program to address a compelling problem. The main objective is to create two distinct models: one leveraging Automated Machine Learning (AutoML) and the other a customized model with hyperparameters tuned using HyperDrive. The performance of both models will be compared, and the best-performing model will be deployed.

Key aspects of the project include:

* Utilizing an external dataset within the workspace.
* Training models using various tools provided by the AzureML framework.
* Comparing the performance of the AutoML model and the customized model.
* Deploying the top-performing model as a web service.

#### The challenges in this project which I can think are:
* Data Quality and Preprocessing: Ensuring dataset cleanliness, handling missing values, outliers, and preprocessing tasks like feature encoding and normalization.

* Model Selection and Tuning: Choosing suitable algorithms, tuning hyperparameters effectively, and balancing model complexity for optimal performance.
  
* Model Evaluation and Interpretability: Assessing model performance, selecting appropriate evaluation metrics, and interpreting results comprehensively.

## Dataset

### Overview


The data I used is from Kaggle which Heart Failure Dataset. The dataset description is given below.
The "Heart Failure Clinical Data" dataset can be used to train various machine learning (ML) models for predictive analytics tasks. One of the use case is:

Binary Classification: This dataset can be used to train binary classification models to predict whether a patient is at risk of death due to heart failure within a certain time frame (e.g., during the follow-up period). Models can be trained to classify patients into two categories: those who are at high risk of death and those who are not.


| Feature                           | Description                                                                                                                                                 |
|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Age                               | This feature represents the age of the patient in years. Age can be an important factor in understanding the risk and prognosis of heart failure, as the incidence of heart failure increases with age.                                                                                                                               |
| Anaemia                           | Anaemia is a condition characterized by a deficiency of red blood cells or hemoglobin in the blood, resulting in reduced oxygen-carrying capacity. This feature indicates whether the patient has anaemia (1 for yes, 0 for no).                                                                                          |
| High Blood Pressure (Hypertension) | High blood pressure, or hypertension, is a common risk factor for heart failure. This feature indicates whether the patient has high blood pressure (1 for yes, 0 for no).                                                                               |
| Smoking                           | This feature indicates whether the patient is a smoker (1 for yes, 0 for no). Smoking is a known risk factor for various cardiovascular diseases, including heart failure.                                                                                           |
| Diabetes                          | Diabetes is a chronic condition characterized by elevated blood sugar levels. This feature indicates whether the patient has diabetes (1 for yes, 0 for no). Diabetes is a significant risk factor for developing heart failure.                                                                                            |
| Sex                               | This feature represents the gender of the patient (1 for male, 0 for female). Gender differences may play a role in the incidence, presentation, and outcomes of heart failure.                                                                                                       |
| Serum Creatinine                 | Serum creatinine is a blood test that measures kidney function. Elevated levels of serum creatinine may indicate impaired kidney function, which can be associated with heart failure and other cardiovascular diseases.                                                                                                           |
| Serum Sodium                     | Serum sodium levels in the blood can indicate hydration status and electrolyte balance. Abnormal serum sodium levels may be associated with heart failure and other cardiovascular conditions.                                                                                  |
| Ejection Fraction                |Ejection fraction is a measure of the heart's pumping efficiency and is expressed as a percentage. It represents the proportion of blood ejected from the heart with each contraction. A reduced ejection fraction is a hallmark feature of heart failure.                                                 |
| Platelets                        | Platelets are blood cells responsible for blood clotting. Platelet count can provide information about a patient's overall health status and potential risk factors for cardiovascular diseases.                                  |
| Serum Creatinine Phosphokinase (CPK) | Serum CPK is an enzyme found predominantly in the heart, brain, and skeletal muscle. Elevated levels of serum CPK may indicate muscle damage, including heart muscle damage, as seen in conditions like heart attacks.       |
| Diuretic Use                     | This feature indicates whether the patient is on medication for heart failure, specifically diuretics (1 for yes, 0 for no). Diuretics are commonly prescribed to manage fluid retention and symptoms of heart failure.                                             |



### Task
#### The task involves training two models: one using AutoML and the other using HyperDrive with hyperparameter tuning. After training, the performance of both models is compared to determine the best-performing one. Finally, the selected model is deployed for practical use.

### Access
*TODO*: Explain how you are accessing the data in your workspace.

I accessed the dataset which is uploaded on github `from_delimited_files('webURL')` of the `TabularDatasetFactory` Class.

https://github.com/bhupendrasolanki/udacity-capstone/blob/main/heart_failure_clinical_records_dataset.csv

## Automated ML

Configuration and settings used for the Automated ML experiment are described in the table below:

Configuration | Description | Value
------------- | ----------- | -----
experiment_timeout_minutes | This is used as an exit criteria, it defines how long, in minutes, your experiment should continue to run | 20
max_concurrent_iterations | Represents the maximum number of iterations that would be executed in parallel | 5
primary_metric | The metric that Automated Machine Learning will optimize for model selection | accuracy
task | The type of task to run. Values can be 'classification', 'regression', or 'forecasting' depending on the type of automated ML problem | classification
compute_target | The compute target to run the experiment on | trainCluster
training_data | Training data, contains both features and label columns | ds
label_column_name | The name of the label column | Class
n_cross_validations | No. of cross validations to perform | 5 

### Results
*TODO*: What are the results you got with your automated ML model? What were the parameters of the model? How could you have improved it?

#### Confusion Matrix

Class Labels | 0 | 1
------------- | ----------- | -----
0 | 195 | 8
1| 24 | 72

The best model is "LightGBMClassifier"

SR No.| Parameter Name | Value 
------------- | ----------- | -----
1 |boosting_type | gbdt
2|colsample_bytree | 0.6933333333333332
3|learning_rate | 0.05789894736842106
4|max_bin | 70
5|max_depth | 8
6|min_child_weight | 8
7|min_data_in_leaf | 0.041385172413793116
8|min_split_gain | 0.6842105263157894
9|n_estimators | 400
10|num_leaves | 200
11|reg_alpha | 0.5789473684210527
12|reg_lambda | 0.2631578947368421
13|subsample | 0.29736842105263156
        
*TODO* Remeber to provide screenshots of the `RunDetails` widget as well as a screenshot of the best model trained with it's parameters.

#### Below is the completed AutoML run.

![alt text](https://github.com/bhupendrasolanki/udacity-capstone/blob/main/automl_run_complete.PNG)

#### Best model saved.
![alt text](https://github.com/bhupendrasolanki/udacity-capstone/blob/main/best_model_automl.PNG)

## Hyperparameter Tuning
*TODO*: What kind of model did you choose for this experiment and why? Give an overview of the types of parameters and their ranges used for the hyperparameter search.

I have used Logistic Regression for Hyperparameter Tuning Task.
The parameters used are "C" and "max-iter".  "C" is Inverse of regularization strength and max-iter is Maximum number of iterations taken for the solvers to converge.


### Results
*TODO*: What are the results you got with your model? What were the parameters of the model? How could you have improved it?

*TODO* Remeber to provide screenshots of the `RunDetails` widget as well as a screenshot of the best model trained with it's parameters.

![alt text](https://github.com/bhupendrasolanki/udacity-capstone/blob/main/hyper_drive_run_details.PNG)



## Model Deployment
*TODO*: Give an overview of the deployed model and instructions on how to query the endpoint with a sample input.

#### Below is the best model service.
![alt text](https://github.com/bhupendrasolanki/udacity-capstone/blob/main/service_success.PNG)

#### Test data to test service.

![alt text](https://github.com/bhupendrasolanki/udacity-capstone/blob/main/best_model_test_data.PNG)

#### Test Data query endpoint.

![alt text](https://github.com/bhupendrasolanki/udacity-capstone/blob/main/best_model_endpoint_test.PNG)

![alt text](https://github.com/bhupendrasolanki/udacity-capstone/blob/main/deployed_service.PNG)

## Screen Recording

Please find the below link for video.
https://www.youtube.com/watch?v=niPxG80ICyw

## Future Improvements
* Increase model training time to allow for better convergence and exploration of a wider range of algorithms and hyperparameters in AutoML.
* Apply AutoML's model interpretability features on larger and more complex datasets to gain deeper insights into feature importance and model behavior, facilitating refined feature engineering and model architecture.
* Experiment with alternative hyperparameter sampling methods such as Grid or Bayesian sampling on the Logistic Regression model or other machine learning models to identify optimal hyperparameter configurations more efficiently.

