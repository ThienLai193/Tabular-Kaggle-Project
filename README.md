# AMEX Default Prediction Project

## Project Description
This project builds a machine learning model to predict customer default risk using aggregated transaction data.

## Steps Completed
- Data loading and initial exploration
- Data cleaning and missing value handling
- Feature aggregation by `customer_ID`
- One-hot encoding for categorical features
- Train/validation/test split (60/20/20)
- Gradient Boosting model training
- Model evaluation using classification report, confusion matrix, and ROC-AUC
- Submission file generation

## Model
- GradientBoostingClassifier
- Hyperparameters:
  - n_estimators = 200
  - max_depth = 5
  - learning_rate = 0.1
  - subsample = 0.8

## Evaluation
- Accuracy
- Precision & Recall
- Confusion Matrix
- ROC Curve and AUC Score

## Handling Class Imbalance
The dataset is imbalanced due to subsampling of the negative class.  
To address this, sample weights were applied during model training:
- Class 0 (No Default): weight = 20
- Class 1 (Default): weight = 1

## Submission
Predictions were generated for the test set and saved in the required format:

- `customer_ID`
- `prediction`

The output file follows the structure of the provided sample submission file.

## Notes
- The original dataset is very large (~33GB) and cannot be processed locally.
- A sampled subset of the test data was used to demonstrate the pipeline.
- The submission file was created following the provided sample submission format.

## Author
Thien Lai
