# SG-Credit-Fraud-Detection

# Fraud Detection Analysis

This project explores fraud detection in transactional data, using both exploratory data analysis (EDA) and machine learning models. The dataset contains transactions with a very low fraud rate (~0.015%).

---

## 1. Exploratory Data Analysis (EDA)

- **Transaction Type:**  
  Fraud occurs almost entirely in **TRANSFER** transactions. Other types like PAYMENT, CASH_OUT, etc. are mostly non-fraud.  

- **Location:**  
  Locations were randomly assigned (e.g., CBD, Jurong). Fraud is spread evenly across them, so location doesn’t provide useful signals.  

👉 **Key takeaway:** Fraud is rare, but when it happens, it’s concentrated in TRANSFER transactions.

---

## 2. Isolation Forest (Unsupervised Anomaly Detection)

- **AUC ~ 0.49** → performs about the same as random guessing.  
- **Confusion Matrix:**  
  - 1,270,263 true negatives  
  - 2,073 false positives  
  - 188 false negatives  
  - 0 true positives  

👉 **Result:** The model failed to catch any frauds. This happens often in fraud detection because fraudulent transactions can look very similar to normal ones.

---

## 3. XGBoost (Supervised Learning)

- **AUC ~ 0.96** → strong performance.  
- **Classification Report:**  
  - Fraud precision: 0.97  
  - Fraud recall: 0.98  
  - Overall F1-score: ~0.96  

- **Confusion Matrix:**  
  - 1,170,804 true negatives  
  - 101,532 false positives  
  - 183 true positives (frauds caught)  
  - 5 false negatives (frauds missed)  

- **Feature Importance:**  
  - `step` (time in dataset)  
  - `oldbalanceOrg` (sender’s original balance)  
  - `amount`, `oldbalanceDest`, `newbalanceDest`  
  - `type_TRANSFER`  

👉 **Result:** XGBoost successfully learned fraud patterns, catching ~97% of fraud cases.

---

## 4. Summary

- Fraud rate: **~0.015%**  
- Isolation Forest failed (no frauds detected).  
- XGBoost performed very well (AUC 0.96, recall 97%).  
- Key fraud signals: transaction type (TRANSFER), balances, and time step.  

---

## Next Steps

- Try other supervised models (e.g., LightGBM, Random Forest) for comparison.  
- Explore feature engineering around transaction networks.  
- Investigate methods to reduce false positives.  

---
