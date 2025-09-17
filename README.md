# 🚀 Proactive Fraud Detection in Financial Transactions

## 📌 Project Overview

This project focuses on building a **machine learning pipeline** to proactively detect fraudulent transactions in financial data. The dataset contains over **6.3 million transactions** with only **0.13% fraud cases**, making it a highly imbalanced classification problem.

We applied **data cleaning, feature engineering, and model development** (Logistic Regression & LightGBM) to identify fraud patterns and provide actionable business insights.

---

## 📂 Dataset

* **Source:** Provided as part of case study (6,362,620 rows, 11 columns).
* **Features include:**

  * `step` → time in hours (1–744, 30-day simulation)
  * `type` → transaction type (`CASH-IN`, `CASH-OUT`, `TRANSFER`, `PAYMENT`, `DEBIT`)
  * `amount` → transaction amount
  * `oldbalanceOrg`, `newbalanceOrig` → sender balances
  * `oldbalanceDest`, `newbalanceDest` → recipient balances
  * `isFraud` → fraud label (target)
  * `isFlaggedFraud` → flagged by business rule (>200,000 transfer)

---

## ⚙️ Methodology

1. **Data Cleaning & Exploration**

   * Verified no missing values.
   * Identified fraud occurs only in `CASH_OUT` and `TRANSFER`.
   * Handled extreme imbalance (fraud ≈ 0.13%).

2. **Feature Engineering**

   * `errorBalanceOrig` = oldbalanceOrg – amount – newbalanceOrig
   * `errorBalanceDest` = oldbalanceDest + amount – newbalanceDest
   * `amount_over_oldbalanceOrg` = ratio of transaction amount to sender’s balance
   * `amount_over_oldbalanceDest` = ratio to recipient’s balance
   * Extracted **hour/day** from `step`

3. **Model Development**

   * **Baseline:** Logistic Regression (class-weight balanced).
   * **Advanced:** LightGBM with `scale_pos_weight` for imbalance handling.

4. **Evaluation Metrics**

   * ROC-AUC & PR-AUC
   * Confusion Matrix, Classification Report
   * Precision\@K (for top % risky transactions).

---

## 📊 Results

### Logistic Regression (Baseline)

* ROC-AUC: **0.9808**
* PR-AUC: **0.5829**
* Precision low due to imbalance, but recall was strong.

### LightGBM (Final Model)

* ROC-AUC: **0.9970**
* PR-AUC: **0.9955**
* Precision\@0.1%: **99.8%**
* Precision\@0.5%: **59.1%**

✅ Model successfully identifies nearly all fraudulent transactions while minimizing false positives.

---

## 🔑 Key Insights

* Fraudulent transactions often:

  * **Drain sender account** (`amount_over_oldbalanceOrg ≈ 1`)
  * Leave sender balance at **0** (`newbalanceOrig = 0`)
  * Route funds into **dormant/empty accounts** (`oldbalanceDest`, `newbalanceDest`)
  * Involve **large, unusual transfers**
  * Occur at specific **time windows**

---

## 🛡️ Business Recommendations

* Deploy **real-time fraud scoring** (LightGBM pipeline).
* Set **alerts for account-draining transactions**.
* Apply **Multi-Factor Authentication (MFA)** for large transfers.
* Monitor **velocity of transactions** (rapid multiple transfers).
* Continuously track **Precision\@K** to ensure fraud detection effectiveness.

---

## 🛠️ Tech Stack

* Python (Pandas, NumPy, Scikit-learn, LightGBM)
* Jupyter Notebook
* Matplotlib / Seaborn (visualization)

---

## 📌 Files in Repository

* `proactive_fraud_detection.ipynb` → main analysis notebook
* `README.md` → project documentation

---

## ✨ Author

👤 **Chethan Vakiti**

* Data Science Enthusiast | Skilled in Python, SQL, Machine Learning, Power BI
* [LinkedIn]([https://www.linkedin.com/in/chethan-vakiti/])
* [GitHub]([https://github.com/Chethan536])

---

