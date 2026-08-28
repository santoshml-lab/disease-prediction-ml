# Heart Disease Prediction ML

A machine learning classification project that predicts the presence or absence of heart disease using clinical features from the UCI Heart Disease dataset.

The project focuses on model comparison, class distribution, missing-value handling, threshold analysis, error analysis, cross-validation, and model interpretability.

## Objective

The objective of this project is to compare multiple machine learning classification algorithms and select a suitable model for heart disease prediction.

Since this is a screening-oriented classification problem, the project evaluates:

- Precision
- Recall
- F1 Score
- ROC-AUC
- Confusion Matrix

Accuracy is reported as a supporting metric rather than the only performance measure.

## Dataset

The project uses the UCI Heart Disease dataset.

- Samples: 303
- Features: 13
- Target: `num`

The original target was converted into a binary classification target:

- `0` = No Disease
- `1` = Disease Present

### Target Distribution

| Class | Count | Percentage |
|---|---:|---:|
| No Disease | 164 | 54.13% |
| Disease | 139 | 45.87% |

The classes are relatively balanced, so no aggressive resampling technique was required.

## Features

The dataset contains the following features:

- `age`
- `sex`
- `cp`
- `trestbps`
- `chol`
- `fbs`
- `restecg`
- `thalach`
- `exang`
- `oldpeak`
- `slope`
- `ca`
- `thal`

## Data Preprocessing

Missing values were identified in:

- `ca`: 4 missing values
- `thal`: 2 missing values

Missing values were handled using median imputation inside the preprocessing pipeline.

The dataset was divided using an 80/20 stratified train-test split:

- Training samples: 242
- Testing samples: 61

Stratification was used to maintain a similar class distribution in the training and testing sets.

## Models Compared

Three classification algorithms were evaluated:

1. Logistic Regression
2. Random Forest
3. XGBoost

### Model Comparison

| Model | Accuracy | Precision | Recall | F1 Score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 0.8689 | 0.8125 | 0.9286 | 0.8667 | 0.9513 |
| Random Forest | 0.9016 | 0.8667 | 0.9286 | 0.8966 | 0.9610 |
| XGBoost | 0.8852 | 0.8182 | 0.9643 | 0.8852 | 0.9481 |

Random Forest achieved the highest F1 Score and ROC-AUC among the evaluated models.

XGBoost achieved the highest recall.

## Cross-Validation

A stratified 5-fold cross-validation was performed using the Random Forest pipeline.

| Metric | Mean ± Standard Deviation |
|---|---:|
| Precision | 0.8652 ± 0.0348 |
| Recall | 0.7765 ± 0.0552 |
| F1 Score | 0.8172 ± 0.0350 |
| ROC-AUC | 0.9111 ± 0.0229 |

Cross-validation results are reported separately from the final held-out test-set results.

## Final Model

Random Forest was selected as the final model because it provided the strongest overall balance of precision, recall, F1 Score, and ROC-AUC on the held-out test set.

At the selected probability threshold of 0.50:

- Accuracy: 90.16%
- Precision: 86.67%
- Recall: 92.86%
- F1 Score: 89.66%
- ROC-AUC: 96.10%

## Threshold Analysis

Multiple probability thresholds were evaluated to study the trade-off between precision and recall.

The threshold of 0.60 achieved a higher F1 Score:

- Precision: 92.59%
- Recall: 89.29%
- F1 Score: 90.91%

However, threshold 0.50 was selected for the final screening-oriented evaluation.

At threshold 0.50:

- False Positives: 4
- False Negatives: 2

At threshold 0.60:

- False Positives: 2
- False Negatives: 3

Because missing a disease-positive case can potentially be more concerning in a screening context, the 0.50 threshold was preferred even though the 0.60 threshold achieved a slightly higher F1 Score.

## Confusion Matrix

At the selected threshold of 0.50:

```text
                 Predicted
              No Disease  Disease

Actual
No Disease        29          4
Disease            2         26
