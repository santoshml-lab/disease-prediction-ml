# Model Results

## 1. Model Comparison

Three machine learning classification algorithms were evaluated:

- Logistic Regression
- Random Forest
- XGBoost

The evaluation focused on precision, recall, F1 score, and ROC-AUC rather than accuracy alone.

| Model | Accuracy | Precision | Recall | F1 Score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 0.8689 | 0.8125 | 0.9286 | 0.8667 | 0.9513 |
| Random Forest | 0.9016 | 0.8667 | 0.9286 | 0.8966 | 0.9610 |
| XGBoost | 0.8852 | 0.8182 | 0.9643 | 0.8852 | 0.9481 |

## 2. Selected Model

Random Forest was selected as the final model because it achieved the highest F1 score and ROC-AUC while maintaining strong recall.

### Final Performance

At a probability threshold of 0.50:

- Accuracy: 90.16%
- Precision: 86.67%
- Recall: 92.86%
- F1 Score: 89.66%
- ROC-AUC: 96.10%

## 3. Threshold Analysis

Multiple probability thresholds were tested to understand the trade-off between precision and recall.

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

Although threshold 0.60 produced the highest F1 score, threshold 0.50 was selected because this is a screening-oriented task where false negatives may be more concerning than false positives.

## 4. Confusion Matrix

At the selected threshold of 0.50:

```text
                 Predicted
              No Disease  Disease

Actual
No Disease        29          4
Disease            2         26
