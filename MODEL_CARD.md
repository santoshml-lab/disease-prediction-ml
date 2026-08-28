# Model Card — Heart Disease Prediction


## 1. Model Overview

This project is an educational machine learning classification system for predicting the presence or absence of heart disease using the UCI Heart Disease dataset.

Three machine learning algorithms were evaluated:

- Logistic Regression
- Random Forest
- XGBoost

Random Forest was selected as the final model based on its overall held-out test performance.

## 2. Intended Use

The model is intended for:

- Educational machine learning projects
- Demonstrating binary classification
- Comparing classification algorithms
- Studying precision, recall, F1 Score, ROC-AUC, and threshold selection
- Demonstrating model interpretability through feature importance

The model is not intended to replace professional medical evaluation.

## 3. Out-of-Scope Use

This model must NOT be used for:

- Making standalone medical diagnoses
- Deciding whether a patient has heart disease without qualified medical review
- Determining whether a patient should receive or avoid treatment
- Emergency medical decision-making
- Replacing a doctor, cardiologist, or other qualified healthcare professional
- Screening or diagnosing real patients without appropriate clinical validation
- Making insurance, employment, or other high-impact decisions about individuals

Model predictions should never be treated as medical advice.

## 4. Dataset

The project uses the UCI Heart Disease dataset.

Dataset characteristics:

- Total samples: 303
- Features: 13
- Target: binary classification
- No Disease: 164 samples
- Disease: 139 samples

The dataset is relatively small and may not represent the diversity of real-world patient populations.

## 5. Preprocessing

The dataset contained missing values in:

- `ca`: 4 missing values
- `thal`: 2 missing values

Missing values were handled using median imputation inside the machine learning pipeline.

The data was divided using a stratified 80/20 train-test split:

- Training samples: 242
- Testing samples: 61

## 6. Model Performance

The evaluated models produced the following held-out test-set results:

| Model | Accuracy | Precision | Recall | F1 Score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 0.8689 | 0.8125 | 0.9286 | 0.8667 | 0.9513 |
| Random Forest | 0.9016 | 0.8667 | 0.9286 | 0.8966 | 0.9610 |
| XGBoost | 0.8852 | 0.8182 | 0.9643 | 0.8852 | 0.9481 |

Random Forest was selected because it achieved the highest F1 Score and ROC-AUC on the held-out test set.

## 7. Cross-Validation

A stratified 5-fold cross-validation was also performed using the Random Forest pipeline.

| Metric | Mean ± Standard Deviation |
|---|---:|
| Precision | 0.8652 ± 0.0348 |
| Recall | 0.7765 ± 0.0552 |
| F1 Score | 0.8172 ± 0.0350 |
| ROC-AUC | 0.9111 ± 0.0229 |

The difference between cross-validation and held-out test performance indicates that performance can vary across data splits.

## 8. Threshold Selection

Several probability thresholds were evaluated.

A threshold of 0.60 produced a higher F1 Score than 0.50:

- Threshold 0.60 F1 Score: 0.9091
- Threshold 0.50 F1 Score: 0.8966

However, threshold 0.50 was selected because it produced fewer false negatives:

### Threshold 0.50

- False Positives: 4
- False Negatives: 2

### Threshold 0.60

- False Positives: 2
- False Negatives: 3

For a screening-oriented educational analysis, the lower number of false negatives was considered more important than the small improvement in F1 Score.

This threshold choice is specific to this project and should not be interpreted as a clinically validated threshold.

## 9. Confusion Matrix and Clinical Interpretation

At threshold 0.50:

```text
                 Predicted
              No Disease  Disease

Actual
No Disease        29          4
Disease            2         26
