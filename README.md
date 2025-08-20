# Credit Card Fraud Detection
![Fraud Detection](content/Eras-Post-Web.webp)

## About the Dataset
- Source: [Kaggle - Credit Card Fraud Detection](https://www.kaggle.com/mlg-ulb/creditcardfraud)  
- Transactions made by European cardholders (September 2013).  
- Period: 2 days, total **284,807 transactions** with **492 frauds** (~0.172%).  
- Highly imbalanced dataset.  
- Features:  
  - `V1` … `V28` → PCA-transformed features  
  - `Time` → seconds since the first transaction  
  - `Amount` → transaction amount  
  - `Class` → target label (1 = fraud, 0 = non-fraud)  

Because of the imbalance, **AUPRC (Area Under Precision-Recall Curve)** is more meaningful than accuracy. I dont really do any method to generate syntethic data like Swote or maybe GAN, because I want to see the real perfomance of the model.

---

## Modeling Approach
I tested **ensemble gradient boosting models** that are popular for imbalanced classification:  

- **XGBoost** → tree-based boosting, used `scale_pos_weight` to handle imbalance.  
- **CatBoost** → robust and easy to tune.  

---

## Performance (Test Data)

| Model      | AUPRC | Notes |
|------------|-------|-------|
| **XGBoost** | **0.894** | Best, high recall with balanced precision |
| CatBoost   | 0.888 | Almost similar, more stable |

---

## Full Dataset Prediction (XGBoost model)

Evaluation on the entire original dataset:

- **Total samples** : 283,718  
- **Correct predictions** : 283,698  
- **Incorrect predictions** : 20  

### Confusion Matrix Breakdown
- **True Negatives (TN)** : 283,239 → correctly classified non-fraud  
- **False Positives (FP)** : 6 → normal transactions flagged as fraud  
- **False Negatives (FN)** : 14 → fraud missed (potential financial loss)  
- **True Positives (TP)** : 459 → frauds correctly detected  

---

## Insights & Business Impact
- With **AUPRC ≈ 0.90**, the model detects the majority of frauds despite heavy imbalance.  
- Out of **492 actual frauds**, **459 were caught** → recall ≈ 93%.  
- Only **6 false positives** → minimal customer inconvenience.  
- **14 false negatives** → focus for future improvement, since every missed fraud = potential financial loss.  

---

## Conclusion
- **XGBoost slightly outperformed CatBoost** (0.894 vs 0.888 AUPRC).  
- Accuracy alone is misleading in imbalanced data, but confusion matrix shows the model is highly effective.  
