
---

# `RESULTS.md`

```markdown
# Model Results

## 1. Overview

This document contains the detailed evaluation results for the Heart Disease Prediction ML project.

Three classification models were compared:

- Logistic Regression
- Random Forest
- XGBoost

The evaluation focused on precision, recall, F1 Score, and ROC-AUC rather than accuracy alone.

## 2. Dataset

- Total samples: 303
- Features: 13
- Training samples: 242
- Testing samples: 61

### Target Distribution

| Class | Count | Percentage |
|---|---:|---:|
| No Disease | 164 | 54.13% |
| Disease | 139 | 45.87% |

The target was converted into a binary classification problem where values greater than 0 were mapped to the disease-positive class.

## 3. Model Comparison

| Model | Accuracy | Precision | Recall | F1 Score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 0.8689 | 0.8125 | 0.9286 | 0.8667 | 0.9513 |
| Random Forest | 0.9016 | 0.8667 | 0.9286 | 0.8966 | 0.9610 |
| XGBoost | 0.8852 | 0.8182 | 0.9643 | 0.8852 | 0.9481 |

### Interpretation

Random Forest achieved the highest:

- Accuracy
- F1 Score
- ROC-AUC

XGBoost achieved the highest recall.

Random Forest therefore provided the strongest overall balance for the final held-out test evaluation.

## 4. Five-Fold Cross-Validation

A stratified 5-fold cross-validation was performed using the Random Forest pipeline.

| Metric | Mean ± Standard Deviation |
|---|---:|
| Precision | 0.8652 ± 0.0348 |
| Recall | 0.7765 ± 0.0552 |
| F1 Score | 0.8172 ± 0.0350 |
| ROC-AUC | 0.9111 ± 0.0229 |

The cross-validation results indicate some variation across folds, particularly in recall.

The cross-validation results should not be confused with the final held-out test-set results.

## 5. Final Model Performance

The selected final model is Random Forest.

At a probability threshold of 0.50:

- Accuracy: 90.16%
- Precision: 86.67%
- Recall: 92.86%
- F1 Score: 89.66%
- ROC-AUC: 96.10%

## 6. Threshold Analysis

Multiple thresholds were evaluated to understand the precision-recall trade-off.

| Threshold | Precision | Recall | F1 Score |
|---:|---:|---:|---:|
| 0.20 | 0.5957 | 1.0000 | 0.7467 |
| 0.25 | 0.6364 | 1.0000 | 0.7778 |
| 0.30 | 0.7000 | 1.0000 | 0.8235 |
| 0.35 | 0.7500 | 0.9643 | 0.8438 |
| 0.40 | 0.7941 | 0.9643 | 0.8710 |
| 0.45 | 0.8438 | 0.9643 | 0.9000 |
| 0.50 | 0.8667 | 0.9286 | 0.8966 |
| 0.55 | 0.8667 | 0.9286 | 0.8966 |
| 0.60 | 0.9259 | 0.8929 | 0.9091 |
| 0.65 | 0.9583 | 0.8214 | 0.8846 |
| 0.70 | 0.9524 | 0.7143 | 0.8163 |

Although threshold 0.60 produced the highest F1 Score, threshold 0.50 was selected for the screening-oriented final evaluation.

## 7. Threshold Decision

### Threshold 0.50

- True Negatives: 29
- False Positives: 4
- False Negatives: 2
- True Positives: 26

### Threshold 0.60

- True Negatives: 31
- False Positives: 2
- False Negatives: 3
- True Positives: 25

The 0.50 threshold was selected because it resulted in fewer false negatives.

For a screening-oriented task, a false negative may be more concerning than a false positive because a potentially affected patient could fail to be flagged.

Therefore, the project prioritizes maintaining strong recall rather than selecting the threshold solely based on the highest F1 Score.

## 8. Confusion Matrix

At threshold 0.50:

```text
                 Predicted
              No Disease  Disease

Actual
No Disease        29          4
Disease            2         26     2         26
