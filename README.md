# Heart Disease Prediction ML

A machine learning project for predicting the presence or absence of heart disease using clinical features from the UCI Heart Disease dataset.

## Project Objective

The goal of this project is to compare multiple machine learning classification algorithms and build a model that can identify patients who may belong to the disease-positive class.

Because this is a screening-oriented problem, recall and false-negative errors are given particular attention rather than relying on accuracy alone.

## Dataset

This project uses the UCI Heart Disease dataset.

- Samples: 303
- Features: 13
- Target: `num`
- Binary target:
  - `0` = No Disease
  - `1` = Disease Present

The original target values greater than 0 were converted to the disease-positive class.

## Data Preprocessing

The dataset contained missing values in:

- `ca`: 4 missing values
- `thal`: 2 missing values

Missing values were handled using median imputation inside a preprocessing pipeline.

The data was split using an 80/20 stratified train-test split.

- Training samples: 242
- Testing samples: 61

## Models Compared

Three classification algorithms were evaluated:

1. Logistic Regression
2. Random Forest
3. XGBoost

The models were evaluated using:

- Accuracy
- Precision
- Recall
- F1 Score
- ROC-AUC

## Model Comparison

| Model | Accuracy | Precision | Recall | F1 Score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 0.8689 | 0.8125 | 0.9286 | 0.8667 | 0.9513 |
| Random Forest | 0.9016 | 0.8667 | 0.9286 | 0.8966 | 0.9610 |
| XGBoost | 0.8852 | 0.8182 | 0.9643 | 0.8852 | 0.9481 |

Random Forest achieved the highest F1 score and ROC-AUC among the three models, while XGBoost achieved the highest recall.

## Final Model

Random Forest was selected as the final model because it provided the best overall balance of precision, recall, F1 score, and ROC-AUC.

At a probability threshold of 0.50:

- Accuracy: 90.16%
- Precision: 86.67%
- Recall: 92.86%
- F1 Score: 89.66%
- ROC-AUC: 96.10%

## Threshold Selection

Thresholds from 0.20 to 0.70 were evaluated.

At threshold 0.50:

- False Positives: 4
- False Negatives: 2
- Precision: 86.67%
- Recall: 92.86%
- F1 Score: 89.66%

At threshold 0.60:

- False Positives: 2
- False Negatives: 3
- Precision: 92.59%
- Recall: 89.29%
- F1 Score: 90.91%

A threshold of 0.50 was selected because this is a screening-oriented task where missing a disease-positive case can potentially be more concerning than generating an additional false positive.

## Confusion Matrix

At the final threshold of 0.50:

```text
                 Predicted
              No Disease  Disease

Actual
No Disease        29          4
Disease            2         26
